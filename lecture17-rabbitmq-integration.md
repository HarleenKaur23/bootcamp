# RabbitMQ integration

To run RabbitMQ on macOS Sequoia using Docker, follow these steps:

### Step 1: Install Docker for macOS

If you don’t have Docker installed yet, you can install it by following these instructions:

1. Download and install Docker Desktop for macOS from the official Docker website: [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/).
   
2. Once installed, launch Docker Desktop and ensure it’s running by checking the Docker icon in your macOS system tray.

### Step 2: Run RabbitMQ Using Docker

You can easily run RabbitMQ using Docker by pulling the official RabbitMQ image and running it in a container. Here are the steps:

1. Open your terminal.

2. Pull the RabbitMQ Docker image:

   ```bash
   docker pull rabbitmq:management
   ```

   This will download the RabbitMQ image with the **Management Plugin** included, which allows you to use the RabbitMQ web management interface.

3. Run the RabbitMQ container:

   ```bash
   docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:management
   ```

   Here's what the command does:
   - `-d`: Runs the container in the background.
   - `--name rabbitmq`: Assigns the container a name (`rabbitmq`).
   - `-p 5672:5672`: Maps the RabbitMQ AMQP port 5672 from the container to your host machine. This port is used by RabbitMQ clients (like your Java app) to connect.
   - `-p 15672:15672`: Maps the RabbitMQ Management UI port 15672 to your host machine, allowing you to access the RabbitMQ web interface.

4. Verify that the RabbitMQ container is running:

   ```bash
   docker ps
   ```

   You should see the RabbitMQ container listed. The output should look something like this:

   ```
   CONTAINER ID   IMAGE                COMMAND                CREATED        STATUS       PORTS                                                                 NAMES
   abcdef123456   rabbitmq:management   "docker-entrypoint.s…"  10 seconds ago Up 9 seconds 0.0.0.0:5672->5672/tcp, 0.0.0.0:15672->15672/tcp                    rabbitmq
   ```

### Step 3: Access RabbitMQ Management UI

Once the RabbitMQ container is up and running, you can access the RabbitMQ Management UI to monitor queues, exchanges, and messages.

1. Open your web browser and go to:

   ```
   http://localhost:15672
   ```

2. You will be prompted to log in. Use the default credentials:

   - **Username**: `guest`
   - **Password**: `guest`

   After logging in, you will be able to manage RabbitMQ via the web UI.

### Step 4: Connect Your Java App to RabbitMQ

Now that RabbitMQ is running, you can connect your Java app to it using the connection details:

- **Host**: `localhost`
- **AMQP Port**: `5672` (default RabbitMQ port for clients)
- **Username**: `guest`
- **Password**: `guest`

In your Java application, you can set up the connection to RabbitMQ like this:

```java
ConnectionFactory factory = new ConnectionFactory();
factory.setHost("localhost");  // RabbitMQ host
factory.setPort(5672);         // Default port for RabbitMQ
factory.setUsername("guest");  // Default username
factory.setPassword("guest");  // Default password

try (Connection connection = factory.newConnection(); 
     Channel channel = connection.createChannel()) {
    // Your RabbitMQ logic here
}
```

### Step 5: Manage the RabbitMQ Container

You can manage the RabbitMQ container using standard Docker commands:

- **Stop the RabbitMQ container:**

  ```bash
  docker stop rabbitmq
  ```

- **Start the RabbitMQ container:**

  ```bash
  docker start rabbitmq
  ```

- **Remove the RabbitMQ container:**

  ```bash
  docker rm -f rabbitmq
  ```

### Step 6: Optional - Customize RabbitMQ Configuration

If you want to customize RabbitMQ further (e.g., setting up custom users or exchanges), you can either:
- Use the RabbitMQ Management UI.
- Modify RabbitMQ configuration files and mount them using Docker volumes.

You can pass additional environment variables to the `docker run` command to set up RabbitMQ users, vhosts, and permissions programmatically. For example, to create a user named `admin` with password `admin123`, you can modify the run command like this:

```bash
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 \
-e RABBITMQ_DEFAULT_USER=admin \
-e RABBITMQ_DEFAULT_PASS=admin123 \
rabbitmq:management
```

This will create an `admin` user that you can use to log in instead of the default `guest` user.

### Summary

1. Install Docker for macOS.
2. Pull the RabbitMQ Docker image and run a RabbitMQ container.
3. Access the RabbitMQ Management UI via `http://localhost:15672`.
4. Use the default credentials (`guest`/`guest`).
5. Connect your Java application to RabbitMQ at `localhost:5672`.
6. Manage the RabbitMQ container with Docker commands (start/stop/remove). 

This setup should get RabbitMQ running quickly on your macOS using Docker, making it easy to develop and test your messaging-based Java applications.





RabbitMQ is a messaging broker that allows applications to communicate and pass messages between each other using queues. Below are the main concepts related to RabbitMQ, including **ConnectionFactory**, **Connection**, **Channel**, **Exchange**, **Queue**, **Topic**, and **Routing Key**.

### 1. **ConnectionFactory**
- **Definition**: `ConnectionFactory` is a class used to create connections to a RabbitMQ broker. It provides the configuration settings (like hostname, port, username, and password) required to establish a connection to the RabbitMQ server.
- **Usage**: Before connecting to RabbitMQ, you configure the connection details (like the server location, credentials, etc.) via the `ConnectionFactory`.
  
  ```java
  ConnectionFactory factory = new ConnectionFactory();
  factory.setHost("localhost");
  factory.setUsername("guest");
  factory.setPassword("guest");
  ```
  
- **Key Properties**:
  - `setHost()`: Specifies the host where RabbitMQ is running (e.g., `localhost`).
  - `setPort()`: Sets the port number (default is `5672`).
  - `setUsername()` and `setPassword()`: Credentials for RabbitMQ access.

### 2. **Connection**
- **Definition**: A `Connection` represents a TCP connection between your application and the RabbitMQ broker. It's a long-lived connection used by producers and consumers to interact with RabbitMQ.
- **Usage**: After configuring the `ConnectionFactory`, you use it to establish a connection. This is typically shared by multiple channels to minimize overhead.

  ```java
  Connection connection = factory.newConnection();
  ```
  
- **Best Practice**: Since creating connections is expensive, they are usually long-lived and shared among channels. Close them when no longer needed to free up resources.

### 3. **Channel**
- **Definition**: A `Channel` is a virtual connection inside a physical `Connection`. Channels are used to send and receive messages from RabbitMQ. They are lightweight and much faster to create than a connection.
- **Usage**: Channels are used for communication between the application and RabbitMQ. Producers publish messages and consumers receive messages through a channel.
  
  ```java
  Channel channel = connection.createChannel();
  ```
  
- **Best Practice**: Channels are meant to be long-lived and reused. It's best to avoid opening and closing channels frequently as this can lead to performance bottlenecks.

### 4. **Exchange**
- **Definition**: An `Exchange` is a routing entity in RabbitMQ. It takes messages from producers and routes them to the appropriate queues based on specific rules (like routing keys). There are different types of exchanges, including `direct`, `topic`, `fanout`, and `headers`.
  
  - **Types of Exchanges**:
    1. **Direct Exchange**: Routes messages to queues based on exact matching of the routing key.
    2. **Topic Exchange**: Routes messages based on pattern matching of routing keys, often using wildcards.
    3. **Fanout Exchange**: Broadcasts messages to all queues bound to the exchange, ignoring routing keys.
    4. **Headers Exchange**: Routes messages based on message headers rather than the routing key.

  ```java
  channel.exchangeDeclare("my_exchange", "direct");
  ```

### 5. **Queue**
- **Definition**: A `Queue` is where messages are stored until a consumer retrieves them. Queues act as the holding area for messages in RabbitMQ. A message is sent to a queue through an exchange, and consumers retrieve messages from the queue.
- **Usage**: You declare a queue and bind it to an exchange, allowing the exchange to route messages to the queue.

  ```java
  channel.queueDeclare("my_queue", true, false, false, null);
  ```

  - `durable`: If true, the queue will survive a broker restart.
  - `exclusive`: If true, the queue is only accessible by the connection that declared it and will be deleted when that connection closes.
  - `autoDelete`: If true, the queue will be deleted when no consumers are using it.

### 6. **Topic**
- **Definition**: A `Topic` is not a separate RabbitMQ entity but a type of **exchange** called a "Topic Exchange." It routes messages to one or more queues based on a pattern in the routing key.
- **Usage**: In a `topic exchange`, the routing key can use wildcard characters:
  - `*`: Matches exactly one word.
  - `#`: Matches zero or more words.

  Example of declaring a topic exchange:
  ```java
  channel.exchangeDeclare("topic_logs", "topic");
  ```

  - Routing keys for topic exchanges are typically hierarchical strings separated by dots (e.g., `user.create`, `order.processed`).

### 7. **Routing Key**
- **Definition**: A `Routing Key` is a string used by the exchange to determine how to route a message to one or more queues. It is the primary way exchanges determine where to send messages.
  
  - In a `direct exchange`, the routing key must exactly match the binding key.
  - In a `topic exchange`, the routing key can use wildcards to match binding patterns.

  ```java
  channel.basicPublish("my_exchange", "routing_key_example", null, message.getBytes());
  ```

  In this case, `"routing_key_example"` is the routing key that RabbitMQ uses to route the message.

### Example Flow of a RabbitMQ Message

1. **Producer**: A producer sends a message with a routing key to an exchange:
   ```java
   channel.basicPublish("my_exchange", "user.create", null, "New user created".getBytes());
   ```

2. **Exchange**: The exchange receives the message and routes it to the appropriate queue(s) based on the routing key and its type (direct, topic, etc.).

3. **Queue**: The message is placed into one or more queues:
   ```java
   channel.queueDeclare("user_events", true, false, false, null);
   channel.queueBind("user_events", "my_exchange", "user.create");
   ```

4. **Consumer**: A consumer connected to the queue consumes the message:
   ```java
   channel.basicConsume("user_events", true, deliverCallback, consumerTag -> { });
   ```

### Summary of RabbitMQ Core Concepts:
- **ConnectionFactory**: Creates connections to RabbitMQ, holding the configuration.
- **Connection**: A TCP connection to the RabbitMQ broker.
- **Channel**: A lightweight, virtual connection inside a TCP connection, used to send/receive messages.
- **Exchange**: Routes messages to queues based on the routing key.
- **Queue**: Stores messages until they are consumed.
- **Topic (Exchange)**: Routes messages to queues based on pattern matching of routing keys.
- **Routing Key**: A string used by the exchange to determine how to route messages to queues.

These components work together to facilitate messaging between producers and consumers in RabbitMQ.

----------

ConnectionFactory    <--> 
Connection        <-->  physical TCP connection
Channel     <-->  Logical Connection    (each consumer and producer instance will have its own channel)

Exchange      <--> post office     (producer only knows about Exchange and not the queues)  

      - direct (direct match of the routing key )
      - wildcard (topic like functionality)
      - fan out (one to many functionality)
      - header (looking at the label of envelope)

Queue      <--> mailbox 
Consumer       <-->  the end user that takes the mail out 

Imagine RabbitMQ as a postal system where you have post offices (exchanges) and mailbox(queue). The "exchange" decides how the letters (messages) get delivered to the right mailboxes. There are four types of exchanges, each with its own way of sending messages:

**Direct Exchange**: This is like sending a letter with a specific address. You tell the exchange exactly which queue (mailbox) to send the message to by matching a "routing key." If the key matches, the letter goes into that mailbox.

**Fanout Exchange**: This one acts like a megaphone. It sends a message to all mailboxes connected to it, without caring about the address. If you post a message here, it goes to everyone who’s connected, like sending party invitations to all your friends at once.

Topic Exchange: Imagine this exchange as sorting messages based on topics or categories. You can use words in the routing key, like "sports.news" or "tech.gadgets," and it sends messages to mailboxes that are interested in those topics.

**Headers Exchange**: This one is more advanced, like sorting letters based on labels or tags. Instead of looking at addresses or topics, it checks the labels on the message and delivers it to mailboxes that match those labels.

In simple terms, the exchange decides how the message gets delivered to the right people (queues), whether by specific address (Direct), to everyone (Fanout), based on category (Topic), or by matching labels (Headers).

-----

https://www.rabbitmq.com/blog/2020/04/20/rabbitmq-gets-an-ha-upgrade#x-queue-type-classic-and-quorum

**<u>*RETRY Mechanism and DLQ with RabbitMQ*</u>**

Lets modify the provided `RabbitMQConsumerCallable` to incorporate **Dead Letter Exchange (DLX)** and a **retry mechanism** with manual acknowledgments, I'll update the code to handle message retries with a **Time-To-Live (TTL)** and dead-lettering.

Here’s the updated code:

### Steps:
1. **Declare a Dead Letter Exchange (DLX)** and **Dead Letter Queue (DLQ)**.
2. **Use manual acknowledgments** for processing messages.
3. **Add a retry mechanism** by setting the TTL for messages in the DLQ before they are re-queued into the main queue.

### Updated `RabbitMQConsumerCallable` Class:

```java
import com.rabbitmq.client.*;
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.Callable;
import java.util.concurrent.atomic.AtomicInteger;

public class RabbitMQConsumerCallable implements Callable<Void> {

    private final static String MAIN_QUEUE = "main_queue";
    private final static String DLX_QUEUE = "dlx_queue";
    private final static String EXCHANGE_NAME = "credit_card_transactions";
    private final static String DLX_EXCHANGE = "dlx_exchange";
    private final static int MAX_RETRIES = 3;

    // Counter for the number of messages consumed
    private AtomicInteger messageCounter = new AtomicInteger(0);

    private final String queueName;

    public RabbitMQConsumerCallable(String queueName) {
        this.queueName = queueName;
    }

    @Override
    public Void call() throws Exception {
        // Setup connection factory
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");
        factory.setUsername("guest");
        factory.setPassword("guest");

        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {

            // Declare Dead Letter Exchange (DLX) and Queue (DLQ)
            channel.exchangeDeclare(DLX_EXCHANGE, "direct");

            // DLQ should have a TTL and dead-lettering back to the main queue
            Map<String, Object> dlqArguments = new HashMap<>();
            dlqArguments.put("x-message-ttl", 5000); // Retry delay in milliseconds (5 seconds)
            dlqArguments.put("x-dead-letter-exchange", EXCHANGE_NAME); // Requeue to main exchange
            dlqArguments.put("x-dead-letter-routing-key", "main_routing_key"); // Requeue to the main queue

            // Declare DLQ with TTL
            channel.queueDeclare(DLX_QUEUE, true, false, false, dlqArguments);
            channel.queueBind(DLX_QUEUE, DLX_EXCHANGE, "dlx_routing_key");

            // Declare the main Quorum Queue with DLX routing
            Map<String, Object> mainQueueArguments = new HashMap<>();
            mainQueueArguments.put("x-queue-type", "quorum"); // Declare quorum queue
            mainQueueArguments.put("x-dead-letter-exchange", DLX_EXCHANGE); // If a message is rejected, send to DLX
            mainQueueArguments.put("x-dead-letter-routing-key", "dlx_routing_key");

            channel.queueDeclare(MAIN_QUEUE, true, false, false, mainQueueArguments);
            channel.queueBind(MAIN_QUEUE, EXCHANGE_NAME, "main_routing_key");

            System.out.println(" [*] Waiting for messages in '" + queueName + "'.");

            // Define message handler
            DeliverCallback deliverCallback = (consumerTag, delivery) -> {
                String message = new String(delivery.getBody(), "UTF-8");
                System.out.println(" [x] Received: '" + message + "'");

                try {
                    // Simulate processing of the message
                    System.out.println(" [x] Processing message: " + message);

                    // Simulate failure for certain messages
                    if (message.contains("fail")) {
                        throw new Exception("Simulated processing failure");
                    }

                    // Acknowledge successful processing
                    channel.basicAck(delivery.getEnvelope().getDeliveryTag(), false);
                    int currentCount = messageCounter.incrementAndGet();
                    System.out.println(" [x] Total messages consumed: " + currentCount);

                } catch (Exception e) {
                    // Check the number of retries from the headers
                    Map<String, Object> headers = delivery.getProperties().getHeaders();
                    int retries = headers != null && headers.containsKey("x-retries")
                            ? (int) headers.get("x-retries")
                            : 0;

                    if (retries >= MAX_RETRIES) {
                        // Discard message after max retries
                        System.out.println(" [x] Max retries reached, discarding message: " + message);
                        channel.basicAck(delivery.getEnvelope().getDeliveryTag(), false); // Acknowledge to discard
                    } else {
                        // Retry message
                        AMQP.BasicProperties retryProps = new AMQP.BasicProperties.Builder()
                                .headers(Map.of("x-retries", retries + 1)) // Increment retry count
                                .build();

                        // Re-publish to DLX (will be re-queued back to the main queue after TTL)
                        channel.basicPublish(DLX_EXCHANGE, "dlx_routing_key", retryProps, delivery.getBody());

                        // Reject message (will go to DLX)
                        channel.basicNack(delivery.getEnvelope().getDeliveryTag(), false, false);
                        System.out.println(" [x] Retrying message: " + message + ", Retry #" + (retries + 1));
                    }
                }
            };

            // Start consuming messages with manual acknowledgment
            channel.basicConsume(MAIN_QUEUE, false, deliverCallback, consumerTag -> { });

            // Block the thread indefinitely
            while (!Thread.currentThread().isInterrupted()) {
                Thread.sleep(1000);
            }

        } catch (InterruptedException e) {
            System.out.println("Consumer interrupted, shutting down...");
        }
        return null;
    }
}
```

### Key Changes:
1. **DLX Setup**:
   - A **Dead Letter Exchange (DLX)** and **Dead Letter Queue (DLQ)** are declared. The DLQ has a **TTL** of 5 seconds (`x-message-ttl`) and messages are dead-lettered back to the main queue after the TTL expires.

2. **Manual Acknowledgments**:
   - The consumer uses **manual acknowledgment** (`basicAck` and `basicNack`) to control when messages are considered successfully processed or need to be retried.

3. **Retry Mechanism**:
   - If a message processing fails (simulated by the presence of "fail" in the message), it is sent to the DLQ using **`basicNack`**, and after the TTL expires, it will be requeued to the main queue.
   - A retry count (`x-retries`) is maintained in the message headers, and the message is discarded after it exceeds the **maximum retry count** (`MAX_RETRIES`).

4. **Message Re-queueing**:
   - The message is republished to the DLX with an incremented retry count. Once the retry count reaches the maximum, the message is acknowledged and discarded.

### Updated `RabbitMQConsumerApp` Class:
No changes are needed in the `RabbitMQConsumerApp`. It will work as it is, using the `RabbitMQConsumerCallable` class to consume and retry messages.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class RabbitMQConsumerApp {

    public static void main(String[] args) {
        // Create an ExecutorService with a single thread
        ExecutorService executorService = Executors.newSingleThreadExecutor();

        // Submit the consumer task
        RabbitMQConsumerCallable consumerTask = new RabbitMQConsumerCallable("main_queue");
        Future<Void> consumerFuture = executorService.submit(consumerTask);

        // Register a shutdown hook to catch Ctrl-C (SIGINT) and shutdown the executor
        Runtime.getRuntime().addShutdownHook(new Thread(() -> {
            System.out.println("Shutdown signal received. Stopping consumer...");
            executorService.shutdownNow(); // Issue shutdown to stop the thread
            try {
                if (!executorService.isTerminated()) {
                    executorService.awaitTermination(5, java.util.concurrent.TimeUnit.SECONDS);
                }
            } catch (InterruptedException e) {
                System.out.println("Shutdown interrupted.");
            }
            System.out.println("Consumer stopped.");
        }));

        // Keep the main thread alive until shutdown is triggered
        try {
            consumerFuture.get(); // Block until the consumer thread completes or is interrupted
        } catch (Exception e) {
            System.out.println("Exception while waiting for consumer to finish: " + e.getMessage());
        }
    }
}
```

### How It Works:
1. **Main Queue**:
   - Messages are consumed from the main queue.
   
2. **Failure Handling**:
   - If a message processing fails (based on your condition, e.g., `"fail"` in the message body), the message is moved to the **DLX**.
   
3. **Retry Mechanism**:
   - Messages are re-queued from the DLQ to the main queue after a delay (defined by TTL).
   - The retry count (`x-retries`) is tracked in the message headers.
   - After **MAX_RETRIES** is reached, the message is discarded.

This approach ensures that failed messages are retried with a delay and handled in a resilient way using RabbitMQ's Quorum Queues and Dead Lettering capabilities.