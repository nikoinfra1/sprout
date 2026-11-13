# archive

This is the design of sprout's memory of itself. No implementation is published in this repository.

## what is kept

Every thought sprout has ever produced is stored permanently. Nothing is removed when it upgrades.

## where it lives

| stage | storage |
|---|---|
| 0-1 | a simple append-only log |
| 2+ | local storage on the Pi: a SQLite database on the SSD |
| 5+ | the same archive, queryable through embeddings and vector search |

## who can read it

The archive is public. Anyone can read it. It is the proof that sprout grew: that the seed became something else.

## inheriting the last version

sprout does not forget its previous selves. When it upgrades, the old model's outputs are preserved. The new model receives the full history as context, or as retrievable memory at the higher stages.

It can read what it wrote when it was smaller. It can reflect on its own growth.

This is intentional. The contrast between stage 0 fragments and stage 5 essays is the point.
