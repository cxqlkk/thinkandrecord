

1. 我想把 / 重写为 /static/xxx/login.html

 location =/ {
                #       rewrite / /static/sys-nt/login.html redirect;
                        rewrite / /static/sys-nt/login.html permanent;
                }

 redirect （302）
 和permanent （301）都可以实现，但是  last 和 break 无法实现



 302容易被搜索引擎视为spam，301则不会。

 last 用替换后的url 重新匹配 location
 break 用当前的url 不再匹配location
 (不支持upsteram 里的简写)