# TAG ?= $(shell git log --format="%H" -n 1)
TAG=v1.2.9

build:
	docker build --tag gotafire/janusec:${TAG} -f Dockerfile .