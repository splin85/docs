# Linux Nat分析

# Nat 
## Nat 原理 
    本设备实现了outbound及server两种Nat：
    outbound: 为SNAT，接口发送的报文会进行源IP-PORT替换
    server:   为DNAT，接口接收的报文会进行目的IP-PORT替换
    
### Nat outbound(SNAT) 添加
    1. 进入vlan接口，配置Nat outbound
        fhos(config)# interface vlan 1
        fhos(config-vlan-1)# nat outbound 192.168.12.0/24 12345 to 12348 outside 10.0.0.38 12345 to 12348
        
     2. 查看Nat outbound配置
        fhos(config-vlan-1)# do show nat outbound 

        Type        Interface    Protocol    Prefix:Ports                      NAT                               Handle  
        Outbound    v.1          any         192.168.12.0/24:12345-12348       10.0.0.38/32:12345-12348          3

        Total nat outbound rules: 1
         
### Nat server(DNAT) 添加
    1. 进入vlan接口，配置Nat outbound
        fhos(config)# interface vlan 1
        fhos(config-vlan-1)# nat server 10.0.0.38 12349 inside 192.168.13.1 12349
    
    2. 查看Nat server配置
        fhos(config-vlan-1)# do show nat server 

        Type        Interface    Protocol    Prefix:Ports                      NAT                               Handle  
        Server      v.1          any         10.0.0.38/32:12349                192.168.13.1/32:12349             4

        Total nat server rules: 1

## Nat 配置查看
    fhos(config-vlan-1)# do show nat 

    Type        Interface    Protocol    Prefix:Ports                      NAT                               Handle  
    Server      v.1          any         10.0.0.38/32:12349                192.168.13.1/32:12349             4

    Outbound    v.1          any         192.168.12.0/24:12345-12348       10.0.0.38/32:12345-12348          3

    Total nat all rules: 2

## Nat 删除
    Nat 配置删除可以根据Nat handle或者Nat全配置删除
    1. 根据handle删除
        fhos(config)# no nat outbound rule handle 3
    
    2, 根据Nat配置删除
        fhos(config)# interface vlan 1
        fhos(config-vlan-1)# no nat server 10.0.0.38 12349 inside 192.168.13.1 12349
     
    3. 查看Nat配置
        fhos(config-vlan-1)# do show nat 

        Type        Interface    Protocol    Prefix:Ports                      NAT                               Handle  


        Total nat all rules: 0

    4, Nat配置全部删除
        fhos(config)# no nat all rules

## 端口号分配
    void nf_nat_l4proto_unique_tuple(const struct nf_nat_l3proto *l3proto,
				 struct nf_conntrack_tuple *tuple,
				 const struct nf_nat_range *range,
				 enum nf_nat_manip_type maniptype,
				 const struct nf_conn *ct,
				 u16 *rover)
    {
        unsigned int range_size, min, i;
        __be16 *portptr;
        u_int16_t off;

        if (maniptype == NF_NAT_MANIP_SRC)
            portptr = &tuple->src.u.all;
        else
            portptr = &tuple->dst.u.all;

        /* If no range specified... */
        if (!(range->flags & NF_NAT_RANGE_PROTO_SPECIFIED)) {
            /* If it's dst rewrite, can't change port */
            if (maniptype == NF_NAT_MANIP_DST)
                return;

            if (ntohs(*portptr) < 1024) {
                /* Loose convention: >> 512 is credential passing */
                if (ntohs(*portptr) < 512) {
                    min = 1;
                    range_size = 511 - min + 1;
                } else {
                    min = 600;
                    range_size = 1023 - min + 1;
                }
            } else {
                min = 1024;
                range_size = 65535 - 1024 + 1;
            }
        } else {
            min = ntohs(range->min_proto.all);
            range_size = ntohs(range->max_proto.all) - min + 1;
        }

        if (range->flags & NF_NAT_RANGE_PROTO_RANDOM) {
            off = l3proto->secure_port(tuple, maniptype == NF_NAT_MANIP_SRC
                              ? tuple->dst.u.all
                              : tuple->src.u.all);
        } else if (range->flags & NF_NAT_RANGE_PROTO_RANDOM_FULLY) {
            off = prandom_u32();
        } else {
            off = *rover;
        }

        for (i = 0; ; ++off) {
            *portptr = htons(min + off % range_size);
            if (++i != range_size && nf_nat_used_tuple(tuple, ct))
                continue;
            if (!(range->flags & NF_NAT_RANGE_PROTO_RANDOM_ALL))
                *rover = off;
            return;
        }
    }
    EXPORT_SYMBOL_GPL(nf_nat_l4proto_unique_tuple);