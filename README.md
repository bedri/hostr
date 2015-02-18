# hostr
Dynamic hostname interpolation and supplement to /etc/hosts

"Oh no, x service is down, I gotta ssh into elrond. What's elrond's IP address again?" 

You have a bunch of machines in the cloud. They come and go so often (livestock, not pets) so you don't bother putting their IPs in /etc/hosts. If only there was a way for your dev machine to automatically know the address to your VMs in the cloud, and connect to them quickly without you needing the IP address. Oh no way, this project does just that? Killer sick, dude.

## Example usage

    $ ssh core@$(hostr elrond)

    $ ssh user@$(hostr my-vps2)
    
or
    
    $ ssh core@`hostr my-vps3`
    
hostr uses the power of bash* command substitution. You can use hostr anywhere that uses bash*:

    $ echo "hey pete, if you need to log into the vps named mega-vps, it's IP address is $(hostr mega-vps)" > email.txt


## Installation

### Summary

  - install node.js
  - clone this repo
  - npm install
  - set VULTR_API_KEY in [repo root]/config.json
  - create shell alias for hostr
  - use hostr
  
### Detail

hostr is written in javascript, so node.js is a dependency. Get node here: http://nodejs.org/download/

Once you have node installed, clone hostr from github onto your computer. I like putting it in a directory, ~/scripts.

    $ mkdir ~/scripts
    $ cd ~/scripts
    $ git clone https://github.com/insanity54/hostr
    $ cd hostr
  
Now we need to satisfy some of hostr's javascript dependencies

    $ npm install
    
K, now we need to give hostr some information sources. These sources are your VPS/VM hosting services. hostr queries these sources using their api, and finds the IP address of the host you specify using it's human readable lable. Right now, vultr is the only suported source. We tell hostr about our vultr account by editing the hostr config file, `~/scripts/hostr/config.json`

    {
        "VULTR_API_KEY": "enter your vultr api key here (get it from https://my.vultr.com/settings/) (optional)".
        "DO_CLIENT_ID": "enter your digital ocean client id here (get it from https://cloud.digitalocean.com/api_access) (optional)",
        "DO_API_KEY": "enter your digital ocean api key here (get it from https://cloud.digitalocean.com/api_access) (optional)"
    }
  
Gr8, now we need to make the hostr command available to bash*. We do this by adding an alias to the end of our ~/.bash_aliases file. For other shell aliases, check their docs. Our ~/.bash_aliases file needs this line:

    alias hostr='~/scripts/hostr/hostr.js'
    
But we can automate adding that with the following command:

    $ echo -e "\nalias hostr='~/scripts/hostr/hostr.js'" >> ~/.bash_aliases

Finally, we need to source the ~/.bashrc file so bash knows about the updated ~/.bash_aliases file. (As an alternative, you can restart your terminal.)

    $ source ~/.bashrc
  
That's it! hostr is ready to use. Try it out!

    $ echo "$(hostr my-vps-name)"



## Troubleshooting

hostr saves a log file to [repo root]/log.txt. To save disk space, this file only logs the results of the last command that was run.
    

## Contributing

I don't know if this project is helpful to anyone other than myself, but if it is, cool! Feel free to open issues, suggest features, submit pull requests or just fork and make your own super cool version.


## Author

I'm Chris Grimmett. I do videos on youtube, develop software, and wish I were a cyborg. I'm looking for a job where I can do cool projects like this one. If you like this project and feel like supporting me, here's my deets:

http://grimtech.net/ ::: http://twitter.com/insanity54 ::: http://youtube.com/user/insanity54

I'm sticker bombing my van. Send me a sticker to put on my van, then I’ll send you a different sticker!

    Chris Grimmett
    PO Box 1517
    Spokane Valley, Washington 99037

Amazon wishlist
http://amzn.com/w/3KN7XHRJ3WHKB

Changetip
http://insanity54.tip.me/

Bitcoin
[1JSG6YdLGVq6nY6Q3vpVxVxZ3aAE7oJK1U](bitcoin:1JSG6YdLGVq6nY6Q3vpVxVxZ3aAE7oJK1U)


Stuff I use that you might enjoy:

Vultr.com
http://www.vultr.com/?ref=6822161

Digital Ocean
https://www.digitalocean.com/?refcode=4d9ece557e9e

League of Legends
http://signup.leagueoflegends.com/?ref=53656770aa37b406820010

dropbox
http://db.tt/dtPRnM1p

Ting
https://zk15r23bg48.ting.com/


## Foot notes

`*` also sh, ksh, and whatever the cool kids use these days
