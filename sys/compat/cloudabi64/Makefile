# $FreeBSD$

.include <src.lua.mk>

# Don't use an OBJDIR
.OBJDIR: ${.CURDIR}

MAKESYSCALLS=	../../tools/makesyscalls.lua
SRCS=		syscalls.conf		\
		../../contrib/cloudabi/syscalls64.master
GENERATED=	cloudabi64_proto.h	\
		cloudabi64_syscall.h	\
		cloudabi64_syscalls.c	\
		cloudabi64_sysent.c	\
		cloudabi64_systrace_args.c

all:
	@echo "make sysent only"

# We .ORDER these explicitly so that we only run MAKESYSCALLS once, rather than
# potentially once for each ${GENERATED} file.
.ORDER: ${GENERATED}
sysent: ${GENERATED}

${GENERATED}: ${MAKESYSCALLS} ${SRCS}
	${LUA} ${MAKESYSCALLS} \
	    ../../contrib/cloudabi/syscalls64.master syscalls.conf
