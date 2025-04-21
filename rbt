if [ $# -eq 0 ]; then
    echo "Usage: $0 <menuentry>"
    exit 1
fi

ENTRY=$(awk -F\' '/menuentry / {print $2}' /boot/grub/grub.cfg  | awk -v pattern="^$1.*" '$0 ~ pattern { print $0; exit}')
echo "Selected entry: $ENTRY"

if [ -z "${ENTRY}" ]; then
    echo "No matching entry found."
    exit 1
fi
ESCAPED_ENTRY=$(printf '%s\n' "$ENTRY" | sed -e 's/[\/&]/\\&/g')

sed -i "s/GRUB_DEFAULT=.*/GRUB_DEFAULT='$ESCAPED_ENTRY'/" /etc/default/grub

update-grub

