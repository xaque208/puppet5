# $FreeBSD: head/databases/puppetdb-terminus3/Makefile 416593 2016-06-09 11:19:58Z romain $

PORTNAME=	puppetdb-terminus3
PORTVERSION=	3.2.4
CATEGORIES=	databases ruby
MASTER_SITES=	http://downloads.puppetlabs.com/puppetdb/
DISTNAME=	puppetdb-${PORTVERSION}

MAINTAINER=	puppet@FreeBSD.org
COMMENT=	PuppetDB storeconfigs backend terminus module

LICENSE=	APACHE20

BUILD_DEPENDS=	puppet:sysutils/puppet4

CONFLICTS_INSTALL=	puppetdb-terminus4-* puppetdb-terminus5-*
USE_RUBY=	yes
NO_BUILD=	yes

do-install:
	${MKDIR} ${STAGEDIR}${RUBY_SITELIBDIR}/puppet
	(cd ${WRKSRC}/puppet && ${COPYTREE_SHARE} . \
		${STAGEDIR}${RUBY_SITELIBDIR}/puppet)

.include <bsd.port.mk>
