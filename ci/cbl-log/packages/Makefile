# cbl-log packaging

ifeq ($(strip $(VERSION)),)
REL_VERSION      = 1.0.0
REVISION     = 9999
else
REL_VERSION  = $(VERSION)
REVISION = $(BUILD_NUMBER)
endif

NAME=couchbase-lite-log
VENDOR='Couchbase Inc.'
INSTALL_PREFIX=/opt/cbl-log
PACKAGE_DESCRIPTION='The cbl-log Tool'
URL='http://couchbase.com'
POST_UNINSTALL_SCRIPT=cbl-log-post-remove.sh

EXCLUDE_FILES='*logtest'

.PHONY: package
package: clean rpm deb1804 deb1604

rpm:
	fpm -s dir -t rpm -n $(NAME) \
		-v $(REL_VERSION) \
		--iteration $(REVISION)_centos7 \
		--prefix $(INSTALL_PREFIX) \
		--chdir install \
		--vendor $(VENDOR) \
		--description $(PACKAGE_DESCRIPTION) \
		--url $(URL) \
		--after-remove $(POST_UNINSTALL_SCRIPT) --debug \
		--exclude $(EXCLUDE_FILES) \
		bin lib
	mv $(NAME)-$(REL_VERSION)*.rpm $(NAME)-$(REL_VERSION)-$(REVISION)-centos7.x86_64.rpm

deb1804:
	fpm -s dir -t deb -n $(NAME) \
		-v $(REL_VERSION) \
		--iteration $(REVISION)-ubuntu18.04 \
		--prefix $(INSTALL_PREFIX) \
		--chdir install \
		--vendor $(VENDOR) \
		--description $(PACKAGE_DESCRIPTION) \
		--url $(URL) \
		--after-remove $(POST_UNINSTALL_SCRIPT) --debug \
		--exclude $(EXCLUDE_FILES) \
		--depends multiarch-support \
		--depends "libc++-dev >= 3.9" \
		--depends libc++abi-dev \
		bin

deb1604:
	fpm -s dir -t deb -n $(NAME) \
		-v $(REL_VERSION) \
		--iteration $(REVISION)-ubuntu16.04 \
		--prefix $(INSTALL_PREFIX) \
		--chdir install \
		--vendor $(VENDOR) \
		--description $(PACKAGE_DESCRIPTION) \
		--url $(URL) \
		--after-remove $(POST_UNINSTALL_SCRIPT) --debug \
		--exclude $(EXCLUDE_FILES) \
		$(DEB_DEPENDENCY) \
		bin lib

clean: 
	rm -f $(NAME)*.rpm $(NAME)*.deb
