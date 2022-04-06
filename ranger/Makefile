
build: clean build_image
	docker run -it --network host --name ranger_builder -v /root:/root ranger mvn clean compile package install

build_image:
	docker build --network host -t ranger .

clean:
	docker rm -f ranger_builder