# $FreeBSD: head/sysutils/facter/Makefile 441494 2017-05-22 22:29:17Z linimon $

PORTNAME=	facter
PORTVERSION=	3.7.1
PORTREVISION?=	0
CATEGORIES?=	sysutils
MASTER_SITES=	http://downloads.puppetlabs.com/facter/

MAINTAINER=	puppet@FreeBSD.org
COMMENT=	Cross-platform library for retrieving facts from OS

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		cmake

.if !defined(PKGNAMEPREFIX)

BROKEN_DragonFly=	DragonFly is not supported upstream
BROKEN_powerpc64=	fails to compile: collection.cc: 'stoi' was not declared in this scope

CONFLICTS_INSTALL=	rubygem-facter-2*

LIB_DEPENDS=	libboost_system.so:devel/boost-libs \
		liblibcpp-hocon.so:devel/cpp-hocon \
		libleatherman_locale.so:devel/leatherman \
		libyaml-cpp.so:devel/yaml-cpp

PLIST_SUB+=	PORTVERSION="${PORTVERSION}"

USE_LDCONFIG=	yes
USE_RUBY=	yes
USES+=		compiler:c++11-lib ssl
CMAKE_ARGS+=	-DMAN_PATH=${MANPREFIX}/man

test: build
	cd ${WRKSRC}/lib && bundle install --path vendor
	cd ${WRKSRC} && ${MAKE} test

.elif ${PKGNAMEPREFIX} == java-

LIB_DEPENDS=	libfacter.so:sysutils/facter

ALL_TARGET=	facter-jruby
USE_JAVA=	yes
JAVA_BUILD=	yes
CMAKE_ARGS+=	-DJAVA_HOME=${JAVA_HOME}

# Ignore sysutils/facter's pkg-plist by providing a non-existent file
PLIST=		${WRKDIR}/no-plist
PLIST_FILES=	${PREFIX}/lib/ruby/vendor_ruby/facter.jar

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/lib/ruby/vendor_ruby
	cd ${WRKSRC} && ${INSTALL_DATA} lib/facter.jar ${STAGEDIR}${PREFIX}/lib/ruby/vendor_ruby

.endif

.include <bsd.port.pre.mk>

.if !defined(PKGNAMEPREFIX) && ${OPSYS} == FreeBSD && ${COMPILER_FEATURES:Mlibstdc++}
BROKEN=		Build with system libstdc++ is unsupported
.endif

.include <bsd.port.post.mk>
