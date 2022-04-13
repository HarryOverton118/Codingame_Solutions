<?php
$cgxLines = array();
$tmp_str = "";
$tabs = 0;
$last_char = "";
$str_started = False;

fscanf(STDIN, "%d", $N);
for ($i = 0; $i < $N; $i++)
{
    $cgxLine = stream_get_line(STDIN, 1000 + 1, "\n");
    array_push($cgxLines, "$cgxLine");
}

## checks to see if current and last char indicate a new line.
function check_next_line($char, $last_char)
{
    global $tabs;
    global $tmp_str;
    if ($last_char == ')' && $char != ';' && $char != ')' && $char != '(')
    {
        $tmp_str .= "\n" . str_repeat("    ", $tabs);
    }
    elseif ($last_char == '(' && $char != ")")
    {
        $tmp_str .= "\n" . str_repeat("    ", $tabs);
    }
    elseif ($last_char == ";")
    {
        $tmp_str .= "\n" . str_repeat("    ", $tabs);
    }
    elseif ($last_char == "=" && $char == "(")
    {
        $tmp_str .= "\n" . str_repeat("    ", $tabs);
    }
}


foreach ($cgxLines as $line)
{
    $line = str_split($line);
    foreach ($line as $char)
    {
        #checks and tracks if we are currently formating a string
        if ($char == "'" && $str_started == False)
        {
            check_next_line($char, $last_char);
            $str_started = True;
            $tmp_str .= $char;
        }
        elseif ($char == "'" && $str_started == True)
        {
            $str_started = False;
            $tmp_str .= $char;
        }
        elseif ($str_started == True)
        {
            $tmp_str .= $char;
        }
        elseif (IntlChar::isspace($char)) #ignore empty spaces
        {
            continue;
        }
        else
        {
            check_next_line($char, $last_char);
            # checks if a new block is starting and updated tabs
            if ($char == "(") 
            {
                $tmp_str .= $char;
                $tabs += 1;
            }
            #checks to see if block is ending and updated tabs
            elseif ($char == ")")
            {
                $tabs -= 1;
                $tmp_str .= "\n" . str_repeat("    ", $tabs) . ")";
            }
            else
            {
                $tmp_str .= $char;
            }
        }
        $last_char = $char;
    }
}

echo $tmp_str;
?>
