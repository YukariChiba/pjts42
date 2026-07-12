FROM coredns/coredns:latest

COPY pjts.dn42.zone mtf.dn42.zone pjts.dn42.rev.zone Corefile /config/

ENTRYPOINT ["/coredns", "-conf", "/config/Corefile"]
