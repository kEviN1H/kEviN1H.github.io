解决问题,首先要了解问题在哪里.\s\s
不管是\s
```julia
Pkg.update()
Pkg.build("WinRPM")
Pkg.add("WinRPM")
```
(或依赖WinRPM的包都会出错)\s
出错如:\s
WARNING: Unknown download failure, error code: 2148270086\s

WARNING: Unknown download failure, error code: 2148270085\s

WARNING: Unknown download failure, error code: 2148270088\s

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
这两个结果是出错代码,是OS的,是什么问题在微软的网站上查\s
https://social.msdn.microsoft.com/Search/en-US?query=-2146697211%200x800c0005&pgArea=header&emptyWatermark=true&ac=5

https://msdn.microsoft.com/en-us/library/ms775145(v=vs.85).aspx

