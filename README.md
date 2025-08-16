# Expose local HTTP Proxies over Cloudflare Tunnel

### Prerequisites

* Server
  * For running your proxy.
* Client:
  * For accessing your proxy.
* Access to Cloudflare Zero Trust:
  * For exposing your proxy to Internet over Cloudflare Infrastructure
    * PS: _You will need an domain pointing to Cloudflare's nameservers._



### Exit node

You will need run the local proxy on your server.&#x20;

For this POC, i will be using a segfault.net instance as exit node:

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>



### Cloudflare and Server Setup

On Cloudflare Dashboard, just go to the Zero Trust:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



Then, Create a tunnel:

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



Select Cloudflared:

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



Is required to name your tunnel:

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>



Copy the tunnel's secret (you can install it, i prefer to always keep the things up on my terminal session only):

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>



Paste and run it on your server:

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>



After that, you will see a new connector on Cloudflare Dashboard. Just go ahead with "Next" button:

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>



Then, chose your domain and type your desidered subdomain:

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



Now, back to your server, start your proxy :

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>



Back to Cloudflare Dashboard, fill with your proxy listener configuration:

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>



Then, click on Complete setup.



### Client Setup

On your client, download the Cloudflared binary and run Cloudflare Tunnel Access:

```
cloudflared access tcp --hostname <subdomain>.<domain> --url <proxy-local-forward>
```

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>



Now, we can check the proxy by `curl` command with `--proxy` parameter:

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>



We can use the proxy on browser too:

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>



This instance on segfault.net has 2 exit nodes, as we see on the [#exit-node](./#exit-node "mention"):

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



Well, this is an simple example. You can use this to multiple scenarios. I have some personal notes that i like to share with you:

* If you are in an controlled environment (your corp, eg.), the network administrator will see that you connected to an Cloudflare's IP, not the exit node&#x20;
