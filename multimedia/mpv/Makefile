COMMENT =		movie player based on MPlayer/mplayer2

GH_ACCOUNT =		mpv-player
GH_PROJECT =		mpv
GH_TAGNAME =		v0.38.0
USE_NOBTCFI =		Yes
REVISION =		0


SHARED_LIBS +=		mpv		2.0

CATEGORIES =		multimedia x11

HOMEPAGE =		https://mpv.io/

# GPLv2+
PERMIT_PACKAGE =	Yes

WANTLIB += ${MODLUA_WANTLIB}
WANTLIB += EGL SDL2 X11 Xext Xpresent Xrandr Xss Xv archive
WANTLIB += ass avcodec avdevice avfilter avformat avutil bluray
WANTLIB += c cdio cdio_cdda cdio_paranoia drm dvdnav iconv jpeg lcms2
WANTLIB += m placebo pthread sndio swresample swscale va va-drm
WANTLIB += va-x11 vulkan z zimg

MODULES =		devel/meson \
			lang/lua \
			lang/python

COMPILER =		base-clang ports-gcc
COMPILER_LANGS =	c

DEBUG_PACKAGES =	${BUILD_PACKAGES}

BUILD_DEPENDS =		audio/ladspa \
			textproc/py-docutils${MODPY_FLAVOR}

LIB_DEPENDS =		archivers/libarchive \
			audio/libcdio \
			audio/libcdio-paranoia \
			converters/libiconv \
			devel/sdl2 \
			graphics/ffmpeg>=4.4.4p5 \
			graphics/jpeg \
			graphics/lcms2 \
			graphics/libplacebo \
			graphics/vulkan-loader \
			graphics/zimg \
			multimedia/libass \
			multimedia/libbluray \
			multimedia/libdvdnav

MODPY_RUNDEP =		No
RUN_DEPENDS =		devel/desktop-file-utils \
			graphics/vulkan-loader \
			www/yt-dlp \
			x11/gtk+4,-guic

CONFIGURE_ARGS =	-Dlua=lua${MODLUA_DEP_VERSION} \
			-Dalsa=disabled \
			-Dandroid-media-ndk=disabled \
			-Daudiounit=disabled \
			-Davfoundation=disabled \
			-Dcaca=disabled \
			-Dcdda=enabled \
			-Dcocoa=disabled \
			-Dcoreaudio=disabled \
			-Dcuda-hwaccel=disabled \
			-Dcuda-interop=disabled \
			-Dd3d9-hwaccel=disabled \
			-Dd3d11=disabled \
			-Dd3d-hwaccel=disabled \
			-Ddirect3d=disabled \
			-Ddmabuf-wayland=disabled \
			-Ddrm=enabled \
			-Ddvbin=disabled \
			-Ddvdnav=enabled \
			-Degl=enabled \
			-Degl-android=disabled \
			-Degl-angle=disabled  \
			-Degl-angle-lib=disabled \
			-Degl-angle-win32=disabled \
			-Degl-drm=disabled \
			-Degl-wayland=disabled \
			-Dgbm=disabled \
			-Dgl-cocoa=disabled \
			-Dgl-dxinterop=disabled \
			-Dgl-dxinterop-d3d9=disabled \
			-Dgl-x11=disabled \
			-Dgl-win32=disabled \
			-Dios-gl=disabled \
			-Djack=disabled \
			-Djavascript=disabled \
			-Dlibmpv=true \
			-Dmacos-cocoa-cb=disabled \
			-Dmacos-media-player=disabled \
			-Dmacos-touchbar=disabled \
			-Dopenal=disabled \
			-Dopensles=disabled \
			-Doss-audio=disabled \
			-Dpipewire=disabled \
			-Dpulse=disabled \
			-Drubberband=disabled \
			-Dsdl2=enabled \
			-Dsdl2-audio=disabled \
			-Dshaderc=disabled \
			-Dsixel=disabled \
			-Dsndio=enabled \
			-Dspirv-cross=disabled \
			-Dswift-build=disabled \
			-Dswift-flags=disabled \
			-Duchardet=disabled \
			-Dvaapi=enabled \
			-Dvaapi-drm=enabled \
			-Dvaapi-x11=enabled \
			-Dvaapi-wayland=disabled \
			-Dvaapi-win32=disabled \
			-Dvapoursynth=disabled \
			-Dvdpau=disabled \
			-Dvdpau-gl-x11=disabled \
			-Dvideotoolbox-gl=disabled \
			-Dvideotoolbox-pl=disabled \
			-Dvulkan=enabled \
			-Dvulkan-interop=disabled \
			-Dwayland=disabled \
			-Dwin32-threads=disabled \
			-Dwasapi=disabled

CFLAGS +=		-I${LOCALBASE}/include
LDFLAGS +=		-L${LOCALBASE}/lib

MODMESON_CONFIGURE_ENV +=	CFLAGS="${CFLAGS}" \
					LDFLAGS="${LDFLAGS}"

NO_TEST =		Yes

post-install:
	mv -f ${PREFIX}/share/doc/mpv ${PREFIX}/share/examples
	${INSTALL_DATA} ${WRKDIST}/TOOLS/mpv_identify.sh \
		${WRKDIST}/TOOLS/umpv ${PREFIX}/share/examples/mpv
	${MODPY_BIN_ADJ} ${PREFIX}/share/examples/mpv/umpv
	mv -f ${WRKINST}${SYSCONFDIR}/mpv/* ${PREFIX}/share/examples/mpv
	sed -Ei 's,(/dev/dvd|/dev/cdrom),/dev/rcd0c,g' ${PREFIX}/man/man1/mpv.1

.include <bsd.port.mk>
