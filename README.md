# ascii-art-justify

A command-line tool written in Go that renders text as ASCII art and lets you control the alignment of the output using the `--align` flag.

---

## Usage

```bash
go run . [OPTION] [STRING] [BANNER]
```

```bash
# Default — left aligned
go run . "hello"

# With alignment flag
go run . --align=left "hello" standard
go run . --align=right "hello" standard
go run . --align=center "hello" shadow
go run . --align=justify "how are you" shadow

# Wrong format — prints usage message
go run . --align right something standard
```

**Available alignments:** `left` `right` `center` `justify`

**Available fonts:** `standard` `shadow` `thinkertoy`

---

## Project Structure

```
ascii-art-justify/
├── main.go
├── functions/
│   ├── generator.go       ← core logic: art generation, alignment, terminal width
│   └── generator_test.go  ← unit tests
└── banners/
    ├── standard.txt
    ├── shadow.txt
    └── thinkertoy.txt
```

---

## How It Works

Every alignment adds spaces before each row of art:

| Alignment | How |
|---|---|
| `left` | No padding — art starts at position 0 |
| `right` | `termWidth - artWidth` spaces before art |
| `center` | `(termWidth - artWidth) / 2` spaces before art |
| `justify` | Spaces distributed evenly between words |

Terminal width is detected at runtime using `tput cols` so the output always adapts to the current terminal size.

---

## Running Tests

```bash
# from inside the functions folder
cd functions
go test -v

# from the project root
go test ./... -v
```

---

## Allowed Packages

Only standard Go packages are used — no external dependencies.

| Package | Used for |
|---|---|
| `os` | Reading files and arguments |
| `os/exec` | Running `tput cols` to get terminal width |
| `fmt` | Printing output |
| `strings` | Text manipulation |
| `strconv` | Converting terminal width string to integer |

## Authors
Emmanuel Usang, Dillon Ofili, Abdulmalik Ojo. 
