## Common Request header

### Host 
- Some web servers host multiple websites so by providing the host headers you can tell it which one you require, otherwise you'll just receive the default website for the serve.

### User-Agent
- This header tells the web server what browser is being used?

### **Content-Length**
- the content length tells the web server how much data to expect in the web request.

### **Accept-Encoding**
- Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.

## **Common Response Headers**
- These are the headers that are returned to the client from the server after a request.

### **Set-Cookie**
- Information to store which gets sent back to the web server on each request.

### **Cache-Control**
- How long to store the content of the response in the browser's cache before it requests it again.

### **Content-Type**
- This header tells the browser what type of data is being returned?

### **Content-Encoding**
- What method has been used to compress the data to make it smaller when sending it over the internet.