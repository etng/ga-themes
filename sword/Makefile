CLI=adm
RESOURCE_PATH=./resource
ASSETS_PATH=./resource/assets

all: assets

# generate assets dist
assets:
	find ./ -name ".DS_Store" -depth -exec rm {} \;
	rm -rf $(ASSETS_PATH)/dist
	mkdir $(ASSETS_PATH)/dist
	mkdir $(ASSETS_PATH)/dist/js
	mkdir $(ASSETS_PATH)/dist/css

	cp -R ./../common/assets/* $(ASSETS_PATH)/src/
	cp $(RESOURCE_PATH)/sword/sword.css $(ASSETS_PATH)/src/css/combine/i_sword.css
	cp $(RESOURCE_PATH)/sword/blue@2x.png $(ASSETS_PATH)/src/css/
	cp $(RESOURCE_PATH)/sword/blue.png $(ASSETS_PATH)/src/css/
	cp $(ASSETS_PATH)/src/js/*.js $(ASSETS_PATH)/dist/js/
	cp $(ASSETS_PATH)/src/css/*.png $(ASSETS_PATH)/dist/css/

	cp -R ./../common/pages/* $(RESOURCE_PATH)/pages/
	cp $(RESOURCE_PATH)/sword/pages/*.tmpl $(RESOURCE_PATH)/pages/
	cp $(RESOURCE_PATH)/sword/pages/components/*.tmpl $(RESOURCE_PATH)/pages/components/
	cp $(RESOURCE_PATH)/sword/pages/components/table/*.tmpl $(RESOURCE_PATH)/pages/components/table/

	cp -R $(ASSETS_PATH)/src/css/fonts $(ASSETS_PATH)/dist/css/
	cp -R $(ASSETS_PATH)/src/img $(ASSETS_PATH)/dist/
	cp -R $(ASSETS_PATH)/src/fonts $(ASSETS_PATH)/dist/

	make combine
	$(CLI) compile asset
	make build-tmpl

	rm -rf $(ASSETS_PATH)/src/*
	rm -rf $(RESOURCE_PATH)/pages/*

combine:
	find ./ -name ".DS_Store" -depth -exec rm {} \;
	make combine-js
	make combine-css

combine-js:
	$(CLI) combine js --src=$(ASSETS_PATH)/src/js/all/ --dist=$(ASSETS_PATH)/dist/js/all.min.js
	$(CLI) combine js --src=$(ASSETS_PATH)/src/js/all_2/ --dist=$(ASSETS_PATH)/dist/js/all_2.min.js
	$(CLI) combine js --src=$(ASSETS_PATH)/src/js/form/ --dist=$(ASSETS_PATH)/dist/js/form.min.js
	$(CLI) combine js --src=$(ASSETS_PATH)/src/js/content/ --dist=$(ASSETS_PATH)/dist/js/content.min.js

combine-css:
	$(CLI) combine css

# generate golang template file
build-tmpl:
	$(CLI) compile tpl -p=sword
