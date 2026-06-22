OUT := out

.PHONY: all clean

all: $(OUT)/relazione.pdf

clean:
	rm -rf $(OUT)

$(OUT)/relazione.pdf: relazione.adoc | $(OUT)
	asciidoctor-pdf $< -o $@ --theme theme.yml -a compress

$(OUT):
	mkdir -p $@
