pacman -Rsn $(pacman -Qdtq)
pacman -Scc
rm /var/lib/systemd/coredump/.
journalctl --vacuum-size=50M
