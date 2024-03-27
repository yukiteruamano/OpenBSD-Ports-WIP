COMMENT =	next-gen tool to impose configurable amount of load

V						= V0.17.06
DIST_TUPLE	+= github ColinIanKing stress-ng ${V} .
CATEGORIES	=	sysutils

HOMEPAGE		= https://github.com/ColinIanKing/stress-ng

MAINTAINER	= Jose Maldonado <josemald89@gmail.com>

# GPLv2+
PERMIT_PACKAGE	=	Yes

WANTLIB += c drm EGL gbm GL GLESv2 gmp jpeg m mpfr pthread X11 X11-xcb
WANTLIB += xcb xcb-dri2 xcb-dri3 xcb-present xcb-randr xcb-sync xcb-xfixes
WANTLIB += xshmfence xxhash z

USE_GMAKE		=	YES
CONFIGURE_STYLE = gnu

BUILD_DEPENDS = devel/libinotify \
								devel/mpfr \
								graphics/jpeg \
								sysutils/xxhash

RUN_DEPENDS =		devel/mpfr \
								graphics/jpeg \
								sysutils/xxhash

CFLAGS	=	-I${LOCALBASE}/include \
					-I${X11BASE}/include

LDFLAGS	= -L${LOCALBASE}/lib/ \
					-L${X11BASE}/lib

MAKE_ENV +=	CFLAGS="${CFLAGS}" \
						LDFLAGS="${LDFLAGS}"

do-configure:
	cd ${WRKSRC} && ${MAKE_ENV} ${GMAKE} ${MAKE_ARGS} ${_MAKE_JOBS} config

do-install:
	${INSTALL_PROGRAM} ${WRKBUILD}/stress-ng ${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/stress-ng.1 ${PREFIX}/man/man1
	${INSTALL_DATA_DIR} ${PREFIX}/share/bash-completion/completions/
	${INSTALL_DATA} ${WRKSRC}/bash-completion/stress-ng \
		${PREFIX}/share/bash-completion/completions/

.include <bsd.port.mk>

