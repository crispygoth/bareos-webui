all: update-pot update-all msgfmt-all

update-pot:
	@(echo 'Updating webui.pot ...';)
	@(find ../../../ -regextype posix-egrep -regex '.*(php|phtml)$$' | grep -v vendor | grep -v tests | xargs xgettext --keyword=translate -L PHP --from-code=UTF-8 -o webui.pot;)

update-po: $(PO)
	@(echo 'Updating $(PO) file ...';)
	@(msgmerge --backup=none -U $(PO) webui.pot)

update-all: webui.pot
	@(echo 'Updating all *.po files ...';)
	@(for i in de_DE en_EN fr_FR ru_RU; do msgmerge --backup=none -U $$i.po $< && touch $$i.po; done;)

msgfmt-all: webui.pot
	@(echo 'Generating all *.mo files ...';)
	@(for i in de_DE en_EN fr_FR ru_RU; do msgfmt $$i.po --output-file=$$i.mo; done;)
