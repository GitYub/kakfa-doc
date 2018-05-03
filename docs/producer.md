
从控制台输入，给名称为：test的topic发送String消息

```
public class Main {
    public static void main(String args[]){

        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");
//        props.put("acks", "all");
//        props.put("retries", 0);
//        props.put("batch.size", 16384);
//        props.put("linger.ms", 1);
//        props.put("buffer.memory", 33554432);
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
//        props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
//        props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

        //生产者发送消息
        String topic = "test";
        Producer<String, String> procuder = new KafkaProducer<String, String>(props);
        for (int i = 1; i <= 10; i++) {
            //String value = "value_" + i;
            Scanner scanner = new Scanner(System.in);
            String value = scanner.next();
            //System.out.println(value);

            ProducerRecord<String, String> msg = new ProducerRecord<String, String>(topic, value);
            procuder.send(msg);
        }
        procuder.flush();

    }
}

```


配合consumer, 运行截图如下

![](./imgs/producer.png)