LIBPATH = ../../../lib
SYSPATH = ../../../sys

all: build

run:
	docker run -it --rm -v $(PWD):/workspace alma-emcc:latest

build:
	emcc -O2 \
		-s EXPORTED_FUNCTIONS=_invokeFunctionsCallback,_updateModeCallback \
		-s ERROR_ON_UNDEFINED_SYMBOLS=0 \
		-o out.js \
		-I. \
		-I $(LIBPATH) \
		-I $(SYSPATH) \
		-D ARCS_MR \
		*.cc $(LIBPATH)/WebXR.cc

start:
	$(eval DIGEST := $(shell shasum -ba 256 out.wasm | cut -d ' ' -f1))
	$(eval DEST := gs://scrap-gcc-emcc/$(DIGEST).bin)
	$(eval URL := https://storage.googleapis.com/scrap-gcc-emcc/$(DIGEST).bin)
	$(eval ARTIFACT := $(shell printf "%s" "$(URL)" | base64 | tr '+/' '-_' | tr -d '='))

	gcloud storage cp out.wasm $(DEST)
	open "https://robot-arm-vr.vercel.app/?artifact=$(ARTIFACT)"
