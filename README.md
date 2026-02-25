pokemonsay : New Generations
==========

![You should try pokemonsay!](res/example.png)

`pokemonsay` is like [`cowsay`][cowsay] but for pokemon only. Internally, `pokemonsay` still uses `cowsay`, so you need it installed too. This repo is a revamp of the original [`pokemonsay`][original_pokemonsay], which looks abandoned now, I'm a big fan of pokemon, so I took the mantle to update it. This version includes all pokemon sprites found in the [PokeSprite Project][pokesprite], including alternate forms (like Shinies, Megas, Alolan, Female Alternates,Galarian and Gigantamax).

Now with Gen 9 Pokemon thanks to the [National Pokedex - Icon Dex][national_pokedex_icon_dex] !

## Dependencies

If you simply want to use `pokemonsay`, the only thing you need installed is `cowsay`. But you are probably interested in `fortune` as well, to provide random sayings to your pokemon.

### Arch Linux

If you use Arch Linux, or other Arch-based distros like me, you can install the dependencies for `pokemonsay` as follows:

```bash
sudo pacman -S fortune-mod cowsay
```

### Ubuntu

 To install them in Ubuntu, simply run :

```bash
sudo apt-get install fortune cowsay
```

## Installation

Keep in mind that `pokemonsay` will only work if you have `cowsay` installed and available in your `$PATH`. To install `pokemonsay` run these commands in a terminal window:

```bash
git clone https://github.com/Prieul-Simon/pokemonsay.git
cd pokemonsay
ln -s <absolute_path>/pokemonthink.sh $HOME/.local/bin/pokemonthink
ln -s <absolute_path>/pokemonsay.sh $HOME/.local/bin/pokemonsay
```

~~After the last command, you will have `pokemonsay` installed in you home folder in `~/.bin/pokemonsay/`. And an symbolic link will be created in `~/bin/pokemonsay`, so that you can have `pokemonsay` in your `$PATH` too.~~\
After the last command, you will have a symbolic link created in `~/.local/bin/pokemonsay`, so that you can have `pokemonsay` in your `$PATH`.

## Usage

Now that you've installed `pokemonsay`, you can make it work like so:

```bash
pokemonsay Hello World
```

To have a random pokemon saying some random thing to you, use `fortune`:

```bash
fortune | pokemonsay
```

And if you really like it, you can add the command above to the end of your `~/.bashrc` file (or equivalent). So you will have a random pokemon speaking to you whenever you open a new terminal window! :D

You get a cowthink-like version too. Try it:

```bash
pokemonthink --pokemon Charmander "Should I wear some clothes?"
```

### Listing all pokemon

You can list all pokemon by passing the `-l` or `--list` flag, like this:

```bash
pokemonsay -l
```

This will print all pokemon and National Dex numbers;

### Selecting specific pokemon

You can select specific pokemon using two flags:
#### `-p` or `--pokemon`

Then you pass the pokemon name, like so:

```bash
pokemonsay -p Pikachu
# Or
pokemonsay --pokemon Pikachu "Pika pika!"
```

_Tip: use `pokemon -l` to see a list of available pokemon_

Using this method you can also specify which form of the pokemon to use.

##### Forms

Some pokemon have alternate forms, such as Mega, Alolan, Galarian, Shiny, Gigantamax, Outfits and Female Forms, to use theses forms you can provide a the full pokemon name and form while using the `-p` or `--pokemon` flag.

- `S` stands for Shiny
- `F` stands for Female
- `FS` stands for Female Shiny

All other forms comes after the pokemon name.

To see a full list of forms, use the flag `-L` or `--listForms`:

```bash
pokemonsay -L | less
```

_(Yes.. that's a lot of forms, over 2600 of them !)_

#### `-d` or `--nationalDex`

You can also pass the National Dex number to get the pokemon, like so:

```bash
# To specify Pikachu
pokemonsay -d 025 "Pika pika!"
```

_Obs.: For this to work, you have to zero-pad the number to 3 places (001 for example)_

Using this, you can select a specific generation using RNG, like so:
```bash
# This will select randomly one of the original 151
pokemonsay -d $(printf "%03d\n" $(shuf -i 1-151 -n 1))
```

_Obs.: This way will always select the base form of the pokemon_

#### `-D` or `--nationalDexForms`

This is like the method above, but it will select a random form each time the command is run

```bash
# To specify Rotom and select a random form
pokemonsay -D 479 "I have multiple forms!"
```

## Building the whole thing

If you want to rebuild everything in the repository,  To install it you will need to build from source. The instructions are provided on their repository. And if you know an easier way, please tell me!

In order to use `pokemonsay` you don't need to build anything because everything is built already within the repository. But if you want to download the whole images again or make some change in the process, you will also need [`img2xterm`][img2xterm] which is used to generate cowfiles from the pokemon images. Here is how it's done:

```bash
# Clone PokeSprite Project and rename them to have the NationalDex number... Thanks PokeSprite maintainers!
sh ./tools/get_pokesprite.sh

# Manipulate the downloaded sprites to trim the useless space around them.
sh ./tools/fix_images.sh

# Use 'img2xterm' to generate .cow files (for 'cowsay').
sh ./tools/make_cowfiles.sh
```

And there it is. Now install it with `install.sh` and you are done.

## NOTICE

Please notice I don't own Pokemon or anything related to it. Pokemon is property of [The Pokemon Company][the_pokemon_company].

[img2xterm]: https://github.com/rossy/img2xterm
[cowsay]: https://en.wikipedia.org/wiki/Cowsay
[original_pokemonsay]: https://github.com/possatti/pokemonsay
[the_pokemon_company]: https://en.wikipedia.org/wiki/The_Pok%C3%A9mon_Company
[pokesprite]: https://github.com/msikma/pokesprite
[national_pokedex_icon_dex]: https://www.deviantart.com/mbcmechachu/art/National-Pokedex-Icon-Dex-824897934
