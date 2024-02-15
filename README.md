## What is Up1-docker
Dockerfile for [Up1](https://github.com/Upload/Up1), a client-side encrypted anonymous file photo hosting service

## How to use Up1-docker

### 1. Clone repo:

```bash
$ cd /opt/
$ git clone https://github.com/ALEXSANPEDRO/Up1-docker.git
$ cd /opt/Up1-docker/
```

### 2. Edit the Dockerfile:

```bash
$ nano Dockerfile
```
<pre>

EXPOSE 9000:9000

ENV HTTP="true" \
	HTTP_LISTEN="0.0.0.0:9000" \
	HTTPS="false" \
	API_KEY="something_really_random" \
	DELETE_KEY="another_random_string" \
	MAX_FILE_SIZE=100000000 \
	SERVER="" \
	FOOTER=""

RUN apt-get install -y git && \
	cd /srv && \
	git clone https://github.com/Upload/Up1 && \
	cd Up1/server && npm install && \
	apt-get remove -y git

WORKDIR /srv/Up1/server

COPY server.conf.template server.conf.template
COPY config.js.template ../client/config.js.template
COPY genconfig.sh genconfig.sh
COPY entrypoint.sh entrypoint.sh

RUN chmod +x genconfig.sh entrypoint.sh

ENTRYPOINT /srv/Up1/server/entrypoint.sh

</pre>

edit:
<pre>
API_KEY="something_really_random" \
DELETE_KEY="another_random_string" \

</pre>
### 3. Save changes

### 4. Rebuild the container:
```bash
$ docker build -t up1 .
```

### 5. Start container:
```bash
$ docker run --name up1 -p 9000:9000 -v /path/to/local/storage/:/srv/Up1/i/ up1
```
HTTPS is not supported cause it intended to use reverse proxy in front container for HTTPS.
