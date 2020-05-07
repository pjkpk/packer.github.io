# servlet
## servlet基本流程
- 客户端（很可能是Web浏览器）通过HTTP提出请求
-  Web服务器接收该请求并将其发给servlet。如果这个servlet尚未被加载，Web服务器将把他加载到Java虚拟机并且执行它。
- servlet将接收该HTTP请求并执行某种处理。
- servlet将向Web服务器返回应答。
- Web服务器将从servlet收回的应答发送给客户端。