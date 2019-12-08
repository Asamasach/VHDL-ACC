----------------------------------------------------------------------------------
-- Company: 
-- Engineer: 
-- 
-- Create Date:    20:57:58 11/18/2016 
-- Design Name: 
-- Module Name:    Acc - Behavioral 
-- Project Name: 
-- Target Devices: 
-- Tool versions: 
-- Description: 
--
-- Dependencies: 
--
-- Revision: 
-- Revision 0.01 - File Created
-- Additional Comments: 
--
----------------------------------------------------------------------------------
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use Ieee.std_logic_unsigned.all;
-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx primitives in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity Acc is
port(
		a,b:in std_logic_vector( 7 downto 0 );
		o: out std_logic_vector( 19 downto 0); -- The max of (out) is 11101110001000001111 so That's enough to consider 20 bit for the result
		clk,clr:in std_logic  
		);
end Acc;

architecture Behavioral of Acc is
signal o_temp:std_logic_vector (19 downto 0);
signal c:std_logic_vector ( 3 downto 0);

begin
process(clk,clr)
	variable prd:std_logic_vector( 15 downto 0 );
	begin
		if (clr = '1') then
		o_temp <= "00000000000000000000";
		elsif (clk'event and clk='1') then
			if c = "1110" then
			o_temp <= "00000000000000000000";
			c <= "0000";
			else
			prd := a*b;
			o_temp<= o_temp+prd; 
			c <= c+1;
			end if;
		end if;
		
end process;
o <= o_temp;


end Behavioral;

