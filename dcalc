using MyQueueLibrary;
using MyStackLibrary;

public class Calculator
{

    


    /// <summary>
    /// In this function it verfies that the parenthesis are balanced. 
    /// It also checks that the operators are balanced. That there is the same number of operators, closed parenthesis
    ///  and opened parenthesis. 
    /// </summary>
    /// <param name="equation"></param>
    /// <returns>It returns true if the parenthesis are balance and falase if it is not balance </returns>
    static public bool CheckParenthesis(string equation)
    {
        int openingCount = 0;
        int closingCount = 0;
        int operatorCount = 0;

        string[] splitEquation = equation.Split(" ");

        for (int i = 0; i < splitEquation.Length; i++)
        {
            if (splitEquation[i] == "(")
            {
                openingCount++;
            }
            else if (splitEquation[i] == ")")
            {
                closingCount++;
            }
            else if (OperatorCheck(splitEquation[i]) == true)
            {
                operatorCount++;
            }
        }

        if (openingCount == closingCount)
        {
            if (operatorCount == openingCount)
            {
                return true;
            }
        }
        else
        {
            return false;
        }

        static bool OperatorCheck(string c)
        {
            string[] arr = { "+", "-", "*", "/", "**", "sin", "cos", "tan", "sqrt" };

            for (int i = 0; i < arr.Length; i++)
            {
                if (arr[i] == c)
                {
                    return true;
                }
            }

            return false;
        }

        return true;
    }

    // Creates a queue of mathematical tokens from a mathematical string
    // Example input:  "( 1 + 2 )"
    // Example output: "(", "1", "+", "2", ")"

    /// <summary>
    /// The function will parse the equation and put it into a queue. 
    /// </summary>
    /// <param name="equation"></param>
    /// <returns> It returns the parsed equation that is now in a queue </returns>
    static public MyQueue<string> ParseEquation(string equation)
    {
        string[] splitEquation = equation.Split(" ");
        MyQueue<string> equationQueue = new MyQueue<string>();

        for (int i = 0; i < splitEquation.Length; i++)
        {
            equationQueue.Enqueue(splitEquation[i]);
        }

        return equationQueue;

    }

    

    /// <summary>
    ///  This function calcualtes the results of the mathematical equation. For example when you when to add two numbers 
    ///  you have to pop off two of the value from the queue and then add those two numbers. 
    ///  The number then needs to to be push onto the stack.
    /// </summary>
    /// <param name="equationTokens"></param>
    /// <returns>It returns the last value from the stack once it is the last token on the stack. </returns>
    static public double Compute(MyQueue<string> equationTokens)
    {
        double numOne = 0;
        double numTwo = 0;
        double temp = 0;

        MyStack<string> operatorStack = new MyStack<string>();
        MyStack<double> numberStack = new MyStack<double>();

        while (equationTokens.Count > 0)
        {
            string value = equationTokens.Dequeue();

            if (double.TryParse(value, out temp) == true)
            {
                numberStack.Push(temp);
            }
            else if (value == ")")
            {
                string op = operatorStack.Pop();

                if (op == "+")
                {
                    numOne = numberStack.Pop();
                    numTwo = numberStack.Pop();

                    numberStack.Push(numOne + numTwo);
                }
                else if (op == "-")
                {
                    numOne = numberStack.Pop();
                    numTwo = numberStack.Pop();

                    numberStack.Push(numTwo - numOne);

                }
                else if (op == "*")
                {
                    numOne = numberStack.Pop();
                    numTwo = numberStack.Pop();

                    numberStack.Push(numOne * numTwo);

                }
                else if (op == "/")
                {
                    numOne = numberStack.Pop();
                    numTwo = numberStack.Pop();

                    numberStack.Push(numTwo / numOne);

                }
                else if (op == "**")
                {
                    numOne = numberStack.Pop();
                    numTwo = numberStack.Pop();

                    numberStack.Push(Math.Pow(numTwo, numOne));

                }
                else if (op == "sqrt")
                {
                    numOne = numberStack.Pop();
                    numberStack.Push(Math.Sqrt(numOne));

                }
                else if (op == "sin")
                {
                    numOne = numberStack.Pop() * (Math.PI / 180);
                    numberStack.Push(Math.Sin(numOne));

                }
                else if (op == "cos")
                {
                    numOne = numberStack.Pop() * (Math.PI / 180);
                    numberStack.Push(Math.Cos(numOne));

                }
                else if (op == "tan")
                {
                    numOne = numberStack.Pop() * (Math.PI / 180);
                    numberStack.Push(Math.Tan(numOne));

                }
            }
            else if (value != "(")
            {
                operatorStack.Push(value);
            }

        }

        return Math.Round(numberStack.Pop(), 4);

    }
}
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Type 'quit' to stop the program.");

        while (true)
        {
            Console.Write("> ");
            string input = Console.ReadLine().ToLower();

            if (input == "quit") { break; }

            if (Calculator.CheckParenthesis(input) == false)
            {
                Console.WriteLine("ERROR: Invalid number of operands and/or operators, " +
                    "please double check equation syntax.");

                continue;
            }

            double finalAnswer = Calculator.Compute(Calculator.ParseEquation(input));

            Console.WriteLine(finalAnswer);
        }


    }
}
