ORG = ankurkatiyar
NAME = log4j-vunerable-server
VERSION = latest
DOCKER_FILE = Dockerfile

.PHONY: build build-nocache tag-latest push push-latest release run

build:
	docker build -t $(ORG)/$(NAME):$(VERSION) -f $(DOCKER_FILE) --rm .

build-nocache:
	docker build -t $(ORG)/$(NAME):$(VERSION) -f $(DOCKER_FILE) --no-cache --rm .

tag-latest:
	docker tag $(ORG)/$(NAME):$(VERSION) $(NAME):latest

push:
	docker push $(ORG)/$(NAME):$(VERSION)

push-latest:
	docker push $(ORG)/$(NAME):latest

run:
	docker run -d -p 8080:8080 -t --name $(NAME) $(ORG)/$(NAME):$(VERSION)

stop:
	docker stop $(NAME) && docker rm $(NAME)

exec:
	docker exec -it $(NAME) bash

logs:
	docker logs $(NAME)


release: build tag-latest push push-latest run
