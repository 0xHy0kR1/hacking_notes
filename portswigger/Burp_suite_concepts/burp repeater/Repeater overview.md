## What is repeater?
- Burp Suite Repeater allows us to craft and/or relay intercepted requests to a target at will.
- In layman's terms, it means we can take a request captured in the Proxy, edit it, and send the same request repeatedly as many times as we wish.
![[burp_basics12.png]]

## General interface of repeater
![[burp_basics21.png]]

1. we have a list of Repeater requests. We can have many different requests going through Repeater: each time we send a new request to Repeater, it will appear up here.
2. Directly underneath the request list, These allow us to send a request, cancel a hanging request, and go forwards/backwards in the request history.
3. Still on the left-hand side of the tab, but taking up most of the window, we have the request and response view. We edit the request in the Request view then press send. The response will show up in the Response view.
4. It is a set of options allowing us to change the layout for the request and response views.
5. At the right-hand side of the window, we have the Inspector, which allows us to break requests apart to analyse and edit them in a slightly more intuitive way than with the raw editor.
6. bove the Inspector we have our target. Quite simply, this is the IP address or domain to which we are sending requests. When we send requests to Repeater from other parts of Burp Suite, this will be filled in automatically.

