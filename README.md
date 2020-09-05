# PyGameUI

PyGameUi (or pgui) is a Python library for creating simple GUI's in pygame

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install PyGameUI.

```bash
pip install pgui
```

You can also install from source this way:
```bash
python3 setup.py install --user
```

## Usage

PyGameUI widgets need a parent class with a screen attribute of type pygame.Surface and an event loop to be used. This is a simple working example:

```python
import pgui
import pygame
import sys

pygame.init()


class Main:
    def __init__(self):
        # Create a screen so we can display our widgets
        self.screen = pygame.display.set_mode((600, 600))

        # Create some widgets
        self.entry = pgui.Entry(self, func=self.clear)
        self.button = pgui.Button(self, func=sys.exit)
        self.print_button = pgui.Button(self, func=self.print_text, text="Print")

        # Modify some widget values
        self.button.set_label("Exit")

        # Move them to the location we want them to be
        self.entry.move(50, 50)
        self.button.move(50, 100)
        self.print_button.move(200, 50)

        # This is optional but we can but the widgets inside a list so we can
        # then iterate through it to update the widgets
        self.widgets = [self.entry, self.button, self.print_button]

    # Define some functions
    def print_text(self):
        # This will print the text typed in the Entry widget
        print(self.entry.text)

    def clear(self):
        # This will clear the text in the Entry widget
        self.entry.clear()

    def update(self):
        self.screen.fill((60, 60, 60))

        # Update each widget
        for w in self.widgets:
            w.update()

        # Update the screen
        pygame.display.flip()

    # We can use a separate method for event handling
    def events(self):
        for event in pygame.event.get():
        # The loop does not need to have anything in it but we
        # can use it however we want

        # for event in pygame.event.get():
        #     if event.type == pygame.QUIT: # Exit if the window closing button is clicked
        #         raise SystemExit  # This is just the same as sys.exit()
        #     if event.type == pygame.KEYDOWN:
        #         if event.key == pygame.K_ESCAPE: # Exit if the 'Esc' key is pressed
        #             raise SystemExit  # This is just the same as sys.exit()


main = Main()
while True:
    main.update()
    main.events()
```

## Documentation
You can read the documentation [here](https://github.com/Kolterdyx/PyGameUI/blob/master/docs/index.md#pygameui-documentation)

## Development
This module is still being developed, and it may be unstable or buggy.

## ChangeLog

You can see the change logs [here](https://github.com/Kolterdyx/PyGameUI/blob/master/CHANGELOG.md)

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
