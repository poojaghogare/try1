
### System 3: Multi-Process Messaging

This project simulates a communication system where messages are split into small chunks and transmitted over UDP. It consists of three distinct components: a **brain**, **ear**, and **mouth**.

### How it Works

**Brain:**

  * Acts as the central controller for the system.
  * Holds the unique ID (like `q1` or `q2`) to distinguish itself from others.
  * Uses the `fork` method to run the ear and mouth at the same time.
  * Provides the menu for you to send messages or check memory.
  * Reads the text files created by the ear to show you what was received.

**Ear:**

  * Runs constantly in the background so it never misses a message.
  * Listens on a specific port for incoming data from other systems.
  * Writes every message it hears directly into a text file.
  * Acts as the system's persistent memory by saving data to disk.
  * Signals the brain whenever a new message arrives so the menu updates.

**Mouth:**

  * Created temporarily only when you need to send a message.
  * Takes the large "User Message" (**um**) that you typed.
  * Splits the **um** into smaller "System Message" (**sm**) chunks of 20 bytes.
  * Adds a header like `[ID:Seq]` to each chunk so they can be tracked.
  * Quits automatically as soon as the message transmission is done.

-----

### Build Instructions

Run the command:

```bash
$ make
```

### How to Run

You need two terminals to simulate two separate systems (`q1` and `q2`).

**Terminal A (System q1):**

```bash
$ ./brain q1 1234
```

**Terminal B (System q2):**

```bash
$ ./brain q2 1235
```

### Usage

  * **Send:** Enter the target port (e.g., `1235`) and your message. The system will automatically chunk the message and send it.
  * **Read:** Displays the contents of the "Ear" memory (saved in `recv_PORT.txt`).
  * **Exit:** Shuts down the background listener and exits.

### Clean Up

To remove executables and memory logs run:

```bash
$ make clean
```

-----
