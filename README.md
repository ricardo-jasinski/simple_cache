# SimpleCache

SimpleCache writes a ruby object to a binary file so that it can be retrieved 
later from the disk rather than recomputed from scratch.

## Usage
SimpleCache defines a single method #load_or_recompute that receives a file path and a 
block. If the file exists and is recent (last changed today), it returns the 
file contents (read with Marshal#load). Otherwise, it executes the block, saves 
its return value (with Marshal#dump) and returns the new data.

```ruby
object = SimpleCache.load_or_recompute('example.dat') do
  # Code that performs a long, computationally expensive task 
  42
end

puts object # => 42
```