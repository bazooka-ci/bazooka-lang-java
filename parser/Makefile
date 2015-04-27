default: image

image: gox
	docker build -t bazooka/parser-java .

gox:
	gox -osarch="linux/amd64" -output="main"
