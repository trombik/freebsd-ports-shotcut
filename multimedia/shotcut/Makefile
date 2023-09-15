PORTNAME=	shotcut
DISTVERSION=	23.07.29
CATEGORIES=	multimedia
MASTER_SITES=	https://github.com/${GH_ACCOUNT}/${PORTNAME}/releases/download/v${DISTVERSION}/
DISTNAME=	${PORTNAME}-src-${DISTVERSION:C/\.//g}

MAINTAINER=	vishwin@FreeBSD.org
COMMENT=	Free, open source, cross-platform video editor
WWW=		https://shotcut.org/

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	libfftw3.so:math/fftw3
RUN_DEPENDS=	ffmpeg:multimedia/ffmpeg \
		${LOCALBASE}/lib/libjack.so:audio/jack \
		${LOCALBASE}/lib/mlt-7/libmltglaxnimate-qt6.so:multimedia/mlt7-glaxnimate@qt6 \
		${LOCALBASE}/lib/mlt-7/libmltqt6.so:multimedia/mlt7-qt@qt6 \
		${LOCALBASE}/lib/libmovit.so:graphics/movit \
		${LOCALBASE}/lib/libmp3lame.so:audio/lame \
		${LOCALBASE}/lib/libvpx.so:multimedia/libvpx \
		${LOCALBASE}/lib/libx264.so:multimedia/libx264

USES=		cmake compiler:c++17-lang cpe desktop-file-utils gl mlt:7 \
		pkgconfig qt:6 sdl shared-mime-info tar:txz xorg
CPE_VENDOR=	meltytech

GH_ACCOUNT=	mltframework

USE_GL=		gl
USE_LOCALE=	C.UTF-8
USE_QT=		base declarative multimedia tools:build
USE_SDL=	sdl2
USE_XORG=	x11
# Needed to be able to correctly check for updates in-app.
CMAKE_ARGS=	-D${PORTNAME:tu}_VERSION="${DISTVERSION}"
CXXFLAGS+=	-DSHOTCUT_NOUPGRADE

SUB_FILES=	wrapper.sh

WRKSRC=		${WRKDIR}/src
WRKSRC_SUBDIR=	${PORTNAME}

OPTIONS_DEFINE=	FREI0R LADSPA NLS
OPTIONS_DEFAULT=FREI0R LADSPA
OPTIONS_SUB=	yes

FREI0R_RUN_DEPENDS=	frei0r-plugins>=0:graphics/frei0r-plugins

LADSPA_RUN_DEPENDS=	swhplugins>=0:audio/swhplugins

post-install:
	${MV} ${STAGEDIR}${PREFIX}/bin/shotcut ${STAGEDIR}${PREFIX}/bin/shotcut-real
	${INSTALL_SCRIPT} ${WRKDIR}/wrapper.sh ${STAGEDIR}${PREFIX}/bin/shotcut

.include <bsd.port.mk>
