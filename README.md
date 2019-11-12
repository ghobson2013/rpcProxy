# rpcProxy v1.0
EOS RPC proxy server

The purpose of this rpc proxy server is to help applications talk to the EOS blockchain without having to worry
about endpoints going offline. 
The proxy server rotates between a chosen list of endpoints , selected via endpoints.js and contains a greylist
that will dynamically get populated if the status codes is > 500

Credit goes to https://github.com/boid-com for writting the original code.

# Install steps for debian/ubuntu based distribution
Note: I have only tested this on ubuntu 18.04 LTS

```
sudo apt install pm2 
chmod +x nodesource_setup.sh
./nodesource_setup.sh
npm i
```

to start the proxy server type:
```
pm2 start ecosystem.config.js
```

you can use **pm2 ls**  to see if its up and running, and **pm2 stop all** , to stop the rpc proxy server.
For security reasons the proxy server will by default only listen on the localhost ( 127.0.0.1 ).
I highly recommend that your application use it as a local service, as there is no authentication.
If you do wish to expose it to external clients you can edit the app.listen() function and simply remove the localhost IP address from it.

To test that it is all running you can try the following:
```
curl --request POST --url http://localhost:3051/v1/chain/get_info
```

If you need any help or have any suggestion don't hesitate to submit in the issues section.

//Gary Hobson
