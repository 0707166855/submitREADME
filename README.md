# submitREADME
class Simulator:
    def __init__(self):
        self.memory = [0] * 0x10000  # initialize memory with all 0s
        self.registers = [0] * 32  # initialize 32 registers with all 0s
        self.pc = 0xCFFF  # program counter starts at 0xCFFF

    def load_program(self, program):
        for i, instruction in enumerate(program):
            self.memory[self.pc + i] = instruction

    def run(self):
        while True:
            instruction = self.memory[self.pc]
            if instruction == "li":
                _, rd, imm = self.memory[self.pc:self.pc+3]
                self.registers[rd] = imm
                self.pc += 3
            elif instruction == "sw":
                _, rs, rt = self.memory[self.pc:self.pc+3]
                self.memory[self.registers[rs]] = self.registers[rt]
                self.pc += 3
            elif instruction == "inc":
                _, rd = self.memory[self.pc:self.pc+2]
                self.registers[rd] += 1
                self.pc += 2
            elif instruction == "bne":
                _, rs, rt, imm = self.memory[self.pc:self.pc+4]
                if self.registers[rs] != self.registers[rt]:
                    self.pc = imm
                else:
                    self.pc += 4
            elif instruction == "halt":
                print("Program halted")
                break
            else:
                print(f"Invalid instruction: {instruction}")
                break
            print(self.registers)  # log register values after every cycle

sim = Simulator()
program = ["li", 0, 0x00000000, "li", 1, 0x0000FFFF, "li", 2, "loop", "sw", 0, 0, "inc", 0, "bne", 0, 1, 2, "halt"]
sim.load_program(program)
sim.run()
## My assignement 
[My link](https://pesapal.freshteam.com/jobs/2OU7qEKgG4DR/junior-developer-23)
