# sscanf

## sscanf 可以用来格式字符串
    返回值为格式化的数量
    
## 例如用sscanf格式化MAC：YY:YY:YY:YY:YY:YY
     int str2mac(const char *str, uint8_t mac[])                                                                                             
     {                                                                                                                                        
         int      i;                                                                                                                          
         int      ret;                                                                                                                        
         char     extra;                                                                                                                      
         uint32_t a[ETH_ALEN];                                                                                                                
                                                                                                                                              
         ret = sscanf(str, "%2x:%2x:%2x:%2x:%2x:%2x%c",                                                                                       
                      a, a + 1, a + 2, a + 3, a + 4, a + 5, &extra);                                                                          
                                                                                                                                              
         if (ret != ETH_ALEN)                                                                                                                 
         {                                                                                                                                    
             return -1;                                                                                                             
         }                                                                                                                                    
                                                                                                                                              
         for (i = 0; i < ETH_ALEN; i++)                                                                                                       
         {                                                                                                                                    
             mac[i] = a[i] & 0xff;                                                                                                            
         }                                                                                                                                    
                                                                                                                                              
         return 0;                                                                                                                  
     } 
     
