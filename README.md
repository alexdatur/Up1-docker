# What is Up1-docker
Dockerfile for [Up1](https://github.com/Upload/Up1), a client-side encrypted file hosting service

# How to use Up1-docker

1. Clone repo: git clone https://github.com/ALEXSANPEDRO/Up1-docker

2. Edit the Dockerfile:
------------------------------------
API_KEY="something_random" \
DELETE_KEY="something_else_random" \
------------------------------------

3. Rebuild the container: docker build -t up1 .

4. Start container: docker run --name up1 -p 9000:9000 -v /path/to/local/storage/:/srv/Up1/i/ up1

HTTPS is not supported cause it intended to use reverse proxy in front container for HTTPS.
