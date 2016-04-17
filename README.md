# text-ip
Have your RPi text you her IP on startup.

This script belongs in `/etc/rc.local`, but make sure you're not completely replacing it. `rc.local` runs after the rest of your stuff has been set up after booting. 

If you have other stuff going on in your rc.local, add the following lines before the final line that reads `exit 0`:


    # Print the IP address
    _IP=$(hostname -I) || true
    if [ "$_IP" ]; then
      printf "My IP address is %s\n" "$_IP"
      IPADDR=$(ifconfig | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}')
    #  replace NUMBER with your cell #
      curl http://textbelt.com/text -d number=NUMBER -d "message= $IPADDR"
    fi
`

Replace "NUMBER" with your phone number in the format 5555555555 (don't include the +1).
