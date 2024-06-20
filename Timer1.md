Timer 1
# Still under development

!#/bin/bash

echo "starting timer1 script"

#frame1
echo -ne "\r <Hello"
sleep .5

#frame2
echo -ne "\r >HellO"
sleep .5

#frame3
echo -ne "\r <Hell0"
sleep .5
echo ""

echo "printf"
printf "/r >Hello"
sleep .5
printf "/r <HellO"
sleep .5
printf "/r >Hello"
sleep .5

echo "finished script"

echo "#####################"
spinner=( Ooooo oOooo ooOoo oooOo ooooO)

copy(){
  echo "Copying files"
  spin &
  pid=$!

  for i in 'seq 1 10'
  do
    sleep 1
  done

  kill $pid
  echo ""
}

spin(){
  while [ 1 ]
  do
    for i in "${spinner[@]}"
    do
      echo -ne "\r$i"
      sleep 0.2
    done
  done
}
copy
