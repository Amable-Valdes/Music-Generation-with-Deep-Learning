# Music Generation with Deep Learning

A neural network that compose music. You can play the example generated in this same repository.

## State
In development
The code with i have trained and used this model is a mess. I'm trying to clean it to push it in the repository but, at the same time, I'm trying to update the architecture to a transformer.

## How it works
In this repository you can find the model. You only need to do:
```python
new_model = tf.keras.models.load_model('model')

states = None
next_char = tf.constant([' '])
result = [next_char]

for n in range(1000):
  next_char, states = new_model.generate_one_step(next_char, states=states)
  result.append(next_char)

result = tf.strings.join(result)
print(result[0].numpy().decode('utf-8'), '\n\n' + '_'*80)
```
It is an RNN so it: generates a music note, return a state and after it you can call generate_one_step with the new state again.

## Translate music as .mid
I recomend use timidity to generate the .mid file:
```bash
sudo apt-get install abcmidi timidity
abc2midi my_file.abc -o my_file.mid && timidity my_file.mid
```
This .mid file can be played ^.^
