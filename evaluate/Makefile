SCALE := 10
JPEG_QF := 10

.PHONY: all setup retrieve

all:

setup: | images
	find download -type f -name "*.zip" -exec unzip -ud images {} \;
	find images -type f -name "*.png" -exec sh -c '\
		ffmpeg -loglevel 0 -y -i "$$1"\
		-q:v $(JPEG_QF)\
		-vf "scale=iw*$(SCALE):ih*$(SCALE):flags=neighbor,\
		     pad=iw+16:ih+16:8:8"\
		"$${1%.png}.jpg"\
		' sh {} \;
	find images -type f -name "*.jpg" -exec sh -c '\
		../restore-pixel-art -o "$${1%.jpg}-restored.png" "$$1"\
		' sh {} \;

retrieve: | download
	wget -O download/1.zip https://opengameart.org/sites/default/files/gfx_3.zip
	wget -O download/2.zip https://opengameart.org/sites/default/files/Icons.zip
	wget -O download/3.zip https://opengameart.org/sites/default/files/lpc_entry.zip
	wget -O download/4.zip https://opengameart.org/sites/default/files/assets_3.zip

download images:
	mkdir -p $@
