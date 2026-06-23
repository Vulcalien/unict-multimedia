SCALE := 10
JPEG_QF := 100

.PHONY: all setup retrieve

all:

run: | images
	find download -type f -name "*.zip" -exec unzip -ud images {} \;
	find images -type f -name "*.png" > list-of-files
	find images -type f -name "*.png" -exec sh -c '\
		convert "$$1"\
		-scale $$(echo $(SCALE)*100 | bc)% -filter point\
		-bordercolor black -border 8\
		-quality $(JPEG_QF)\
		"$${1%.png}.jpg"\
		' sh {} \;
	find images -type f -name "*.jpg" -exec sh -c '\
		../restore-pixel-art -o "$${1%.jpg}-restored.png" "$$1"\
		' sh {} \;
	./results list-of-files

retrieve: | download
	wget -O download/1.zip https://opengameart.org/sites/default/files/gfx_3.zip
	wget -O download/2.zip https://opengameart.org/sites/default/files/Icons.zip
	wget -O download/3.zip https://opengameart.org/sites/default/files/surtizens_0.zip
	wget -O download/4.zip https://opengameart.org/sites/default/files/bosses-pixel-art-sprite-sheet-pack.zip

download images:
	mkdir -p $@
