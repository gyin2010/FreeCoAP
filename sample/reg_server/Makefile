ifeq ($(ip6),y)
IP6_CFLAGS = -DCOAP_IP6
endif
ifneq ($(dtls),n)
DTLS_CFLAGS = -DCOAP_DTLS_EN \
              -DCOAP_CLIENT_AUTH
DTLS_LIBS = -lgmp \
            -lhogweed \
            -lnettle \
            -lgnutls
endif
I1 = ../../lib/include
S1 = ../../lib/src
CC_ ?= gcc
CFLAGS = -Wall \
         -I$(I1)
CFLAGS += $(IP6_CFLAGS)
CFLAGS += $(DTLS_CFLAGS)
LD_ ?= gcc
LDFLAGS =
INCS = reg_server.h \
       registrar.h \
       $(I1)/coap_server.h \
       $(I1)/coap_msg.h \
       $(I1)/coap_log.h \
       $(I1)/coap_ipv.h
OBJS = main.o \
       reg_server.o \
       registrar.o \
       coap_server.o \
       coap_msg.o \
       coap_log.o
LIBS = $(DTLS_LIBS)
PROG = reg_server
RM = /bin/rm -f

$(PROG): $(OBJS)
	$(LD_) $(LDFLAGS) $(OBJS) -o $(PROG) $(LIBS)

main.o: main.c $(INCS)
	$(CC_) $(CFLAGS) -c main.c

reg_server.o: reg_server.c $(INCS)
	$(CC_) $(CFLAGS) -c reg_server.c

registrar.o: registrar.c $(INCS)
	$(CC_) $(CFLAGS) -c registrar.c

coap_server.o: $(S1)/coap_server.c $(INCS)
	$(CC_) $(CFLAGS) -c $(S1)/coap_server.c

coap_msg.o: $(S1)/coap_msg.c $(INCS)
	$(CC_) $(CFLAGS) -c $(S1)/coap_msg.c

coap_log.o: $(S1)/coap_log.c $(INCS)
	$(CC_) $(CFLAGS) -c $(S1)/coap_log.c

clean:
	$(RM) $(PROG) $(OBJS)
