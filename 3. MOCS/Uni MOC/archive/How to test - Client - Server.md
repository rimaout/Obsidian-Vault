---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2026-02-16T09:41
updated: 2026-02-16T09:41
---
For basic testing:
- `make run-server` to start the server
- `make run-client` to start the client

In the make file there is a variable CLIENT_PARAMETERS that can be changed to test different files, try to send:
- a text (`test/how_to_text.md`)
- an audio file (`test/mcr.mp3`)
- a picture (`test/one_piece.jpg`)
- a video (`test/green_day.mp4`)

## Signal Handling

In the client code critical section there is commented sleep(10).

To test the signal handling:
- Uncomment the sleep(10)
- Run the client
- Use Ctrl+C to send SIGINT to the client
- Check the output

## Multiple Concurrent Clients

Run this commands to create te test files:
```shell
yes "File: big_text1.text --- big_text1.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text1.txt

yes "File: big_text2.text --- big_text2.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text2.txt

yes "File: big_text3.text --- big_text3.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text3.txt

yes "File: big_text4.text --- big_text4.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text4.txt

yes "File: big_text5.text --- big_text5.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text5.txt

yes "File: big_text6.text --- big_text6.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text6.txt

yes "File: big_text7.text --- big_text7.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text7.txt

yes "File: big_text8.text --- big_text8.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text8.txt

yes "File: big_text9.text --- big_text9.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text9.txt

yes "File: big_text10.text --- big_text10.textThis is a line of text to make the file bigger." | head -n 1000000 > test/big_text10.txt
```

The to test the concurrency run:
- `make run-server` to start the server
- `make run-10-clients` to start 10 clients (each one with a different file)