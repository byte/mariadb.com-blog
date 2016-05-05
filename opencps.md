# OpenCPS: Vietnam's Public Sector goes Open Source

I'm now in Hanoi, Vietnam, for the launch of [OpenCPS](http://opencps.org.vn/). What might you ask is OpenCPS? OpenCPS translates to Open Core Public Services, as Vietnam is providing online public services and OpenCPS should sit at its core. Naturally, all of this will be opensource, and AGPL licensed. OpenCPS is the first open source project to realize the development of e-government services in Vietnam.

Why does this matter to us? Because at the core of its infrastructure is of course, MariaDB Server as the database of choice, with Red Hat being the Linux provider of choice.

I met the interim project lead, Truong Anh Tuan, quite sometime ago, but the tipping point was a keynote presentation on MariaDB Server at FOSSASIA 2015, in Singapore (so thanks again to the organisers for ensuring I keynoted about MariaDB Server there). So when they approached me at FOSSASIA 2016, I was extremely happy to learn that MariaDB Server was a key part of their infrastructure.

MariaDB Server will of course provide the crucial data storage layer, as one would think that data in databases should last beyond a lifetime. We are in good company on the infrastructure layer, with Red Hat Enterprise Linux/CentOS providing the base OS, and the fact that they are also going to be using Docker containers and OpenLDAP. The front-end is the [NukeViet](https://github.com/nukeviet/nukeviet) CMS.

Some of the features of MariaDB Server that they will be using and benefitting from are not limited to encryption at rest, the PAM plugin, GIS, but also down the line window functions from an analytics standpoint.

The project is on [Github](https://github.com/VietOpenCPS), you can find them on Freenode IRC at #opencps, and they also have a [mailing list](http://lists.opencps.vn/mailman/listinfo). 

I look forward to closely collaborating with OpenCPS going forward. Its always a good day when a government of a nation chooses opensource software.

If you're looking for some pictures, there are some tweets with them -- when something official comes, we'll update the post. [encryption](https://twitter.com/bytebot/status/728076262447554560), [tweet thread](https://twitter.com/bytebot/status/728051669997486081), [Google Summer of Code 2017?](https://twitter.com/harishpillay/status/728071519172091905), [MariaDB 5.2](https://twitter.com/harishpillay/status/728071164854083584).