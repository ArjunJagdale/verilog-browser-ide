# Verilog Compiler IDE (Flask + React)

This is a simple web-based Verilog IDE. You can write Verilog code in the browser, compile it using a Flask backend (with `iverilog`), and see the output instantly. It helps in learning and testing Verilog HDL quickly.

---

## Preview
![ReactApp-Brave2025-07-2412-07-58-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/0a12193b-49a5-43b6-ab23-31087afce54b)
---

## Tech Stack

- **Frontend:** React + Monaco Editor
- **Backend:** Python (Flask)
- **Compiler:** [Icarus Verilog (iverilog)](http://iverilog.icarus.com/)

---

## Features

- Verilog code editor with syntax highlighting
- Compile and run Verilog code with `iverilog` and `vvp`
- Displays errors with line numbers and suggestions
- Shows output from the simulation
- Keyboard shortcut `Ctrl+Enter` to compile
- Simple and responsive UI

---

## Local Setup

### 1. Backend (Flask)

#### Prerequisites:
- Python 3.8 or higher
- `iverilog` installed and available in system PATH

#### Steps:
```bash
cd backend
pip install flask flask-cors
python app.py
````

By default, it runs at `http://localhost:5000`

---

### 2. Frontend (React)

#### Prerequisites:

* Node.js (v18 or newer)
* npm or yarn

#### Steps:

```bash
cd frontend
npm install
npm start
```

The frontend runs at `http://localhost:3000` and calls the backend at port 5000.

---

## API Details

**Endpoint:** `POST /compile`

**Request Body:**

```json
{
  "code": "// Your Verilog code here"
}
```

**Responses:**

* Success:

  ```json
  { "status": "success", "stdout": "...", "stderr": "..." }
  ```

* Compilation Error:

  ```json
  { "status": "compile_error", "errors": [...], "raw": "..." }
  ```

* Runtime Error:

  ```json
  { "status": "runtime_error", "stdout": "...", "stderr": "..." }
  ```

---

## Example Verilog Code

```verilog
module test;
  initial begin
    $display("Hello Verilog!");
  end
endmodule
```

---

## Project Structure

```
verilog-IDE/
├── backend/
│   └── app.py          # Flask backend
├── frontend/
│   ├── App.js          # React frontend
│   └── App.css         # Styles
└── README.md           # This file
```

---

## Known Limitations

* No code history or file saving
* Limited to basic Verilog (no waveform viewer or debugging tools)
* Requires backend to run locally

---

## Sample Verlilog CODE

```Velilog
// 4-bit Ripple Carry Adder

module full_adder (
    input a, b, cin,
    output sum, cout
);
    assign {cout, sum} = a + b + cin;
endmodule

module ripple_carry_adder_4bit (
    input [3:0] A, B,
    input Cin,
    output [3:0] Sum,
    output Cout
);
    wire c1, c2, c3;

    full_adder FA0 (A[0], B[0], Cin,  Sum[0], c1);
    full_adder FA1 (A[1], B[1], c1,   Sum[1], c2);
    full_adder FA2 (A[2], B[2], c2,   Sum[2], c3);
    full_adder FA3 (A[3], B[3], c3,   Sum[3], Cout);
endmodule

// Testbench
module testbench;
    reg [3:0] A, B;
    reg Cin;
    wire [3:0] Sum;
    wire Cout;

    ripple_carry_adder_4bit RCA (
        .A(A), .B(B), .Cin(Cin), .Sum(Sum), .Cout(Cout)
    );

    initial begin
        $display("Time\tA\tB\tCin\tSum\tCout");
        $monitor("%0t\t%b\t%b\t%b\t%b\t%b", $time, A, B, Cin, Sum, Cout);

        A = 4'b0001; B = 4'b0010; Cin = 0; #10;
        A = 4'b0101; B = 4'b0011; Cin = 1; #10;
        A = 4'b1111; B = 4'b1111; Cin = 0; #10;
        A = 4'b1000; B = 4'b1000; Cin = 1; #10;

        $finish;
    end
endmodule

```
## License

MIT License © 2025 [Arjun Jagdale](https://github.com/ArjunJagdale)
