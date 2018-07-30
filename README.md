# Meteor's DDP stream server based on SockJS

> Network core of the Meteor's DDP.

`stream-server` package provide:

* default Meteor's stream server based on SockJS;
* mechanism for replace bundled `StreamServer`.

## How to add your custom `StreamServer` to `StreamServers` and activate it

As example your package have name `custom-stream-server`.

1. Enable access to the `StreamServers` variable.

    `custom-stream-server/package.js`

    ```js
    Package.onUse(function (api) {
      // Add following lines
      api.use(['stream-server'], 'server');
      api.imply(['stream-server'], 'server');
      api.export('StreamServers', 'server');
      // ...
    });
    ```

2. Push `CustomStreamServer` to the `StreamServers` array.

    `custom-stream-server/server.js`

    ```js
    class CustomStreamServer {
      constructor() {
        // this.server = new WebSocket.Server();
      }
    }
    
    StreamServers.push(CustomStreamServer);
    ```

3. Activate your custom stream server.

    In `.meteor/packages` move your package before packages:
    
    * `meteor-tools`
    * `ddp`
    * `ddp-server`

    Example of the `.meteor/packages`
    
    ```
    custom-stream-server
    meteor-tools
    # other packages
    ```