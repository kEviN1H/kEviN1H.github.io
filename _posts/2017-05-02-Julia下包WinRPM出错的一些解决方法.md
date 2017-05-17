### 解决问题,首先要了解问题在哪里.  
不管是  
```julia
Pkg.update()
Pkg.build("WinRPM")
Pkg.add("WinRPM")
```
(或依赖WinRPM的包都会出错)    
出错如:   
WARNING: Unknown download failure, error code: 2148270086  

WARNING: Unknown download failure, error code: 2148270085  

WARNING: Unknown download failure, error code: 2148270088  

WARNING: Unknown download failure, error code: 2148270094    

```julia
julia> UInt32(2148270086)
0x800c0006

julia>  reinterpret(Int32,UInt32(2148270086))
-2146697210

julia> UInt32(2148270085)
0x800c0005

julia>  reinterpret(Int32,UInt32(2148270085))
-2146697211

julia> UInt32(2148270088)
0x800c0008

julia>  reinterpret(Int32,UInt32(2148270088))
-2146697208

julia> UInt32(2148270094)
0x800c000e

julia>  reinterpret(Int32,UInt32(2148270094))
-2146697202

```
这两个结果是出错代码,是OS的,是什么问题在微软的网站上查  
[search: -2146697211 0x800c0005](https://social.msdn.microsoft.com/Search/en-US?query=-2146697211%200x800c0005&pgArea=header&emptyWatermark=true&ac=5)   

[URL Moniker Error Codes](https://msdn.microsoft.com/en-us/library/ms775145(v=vs.85).aspx)  

先找到问题再找解决办法
出错[0x800c0005](https://support.microsoft.com/en-us/help/843499/-error-0x8004005-or-error-0x800c0005-error-messages-when-you-scan-for-updates)   
INET_E_RESOURCE_NOT_FOUND
0x800C0005
The server or proxy was not found.

把代理服务器地址加到machine.config里,文件默认位置C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG   
```xml
  <system.net> 
    <defaultProxy> 
      <proxy usesystemdefault="false" proxyaddress="http://127.0.0.1:8087" bypassonlocal="true" /> 
     </defaultProxy>
  </system.net>
  ```
  
 加到文件最后</configuration>的前面.
 
