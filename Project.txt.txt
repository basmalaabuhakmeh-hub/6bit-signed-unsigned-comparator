module unsigned_comp (input [5:0] A, B,output reg A_greater_B, A_equal_B, A_smaller_B);

	wire [5:0] notA, notB;
	wire [5:0] and_A_notB, and_B_notA;	
	wire [5:0] x;

	wire [4:0] y;
	wire [4:0] z;
	// to get ~A and ~B
	not #(3ns) n1(notA[0], A[0]);
	not #(3ns) n2(notA[1], A[1]); 
	not #(3ns) n3(notA[2], A[2]);
	not #(3ns) n4(notA[3], A[3]);
	not #(3ns) n5(notA[4], A[4]);
	not #(3ns) n6(notA[5], A[5]);
	
	not #(3ns) n7(notB[0], B[0]);
	not #(3ns) n8(notB[1], B[1]); 
	not #(3ns) n9(notB[2], B[2]);
	not #(3ns) n10(notB[3], B[3]);
	not #(3ns) n11(notB[4], B[4]);
	not #(3ns) n12(notB[5], B[5]);
	
	// to do and gates
	and #(6ns) a1(and_B_notA[5], notA[5], B[5]);
	and #(6ns) a2(and_A_notB[5], notB[5], A[5]);
	and #(6ns) a3(and_B_notA[4], notA[4], B[4]);
	and #(6ns) a4(and_A_notB[4], notB[4], A[4]); 
	and #(6ns) a5(and_B_notA[3], notA[3], B[3]);
	and #(6ns) a6(and_A_notB[3], notB[3], A[3]); 
	and #(6ns) a7(and_B_notA[2], notA[2], B[2]);
	and #(6ns) a8(and_A_notB[2], notB[2], A[2]);
	and #(6ns) a9(and_B_notA[1], notA[1], B[1]);
	and #(6ns) a10(and_A_notB[1], notB[1], A[1]);
	and #(6ns) a11(and_B_notA[0], notA[0], B[0]);
	and #(6ns) a12(and_A_notB[0], notB[0], A[0]);  
	
	nor #(4ns) nor1(x[0], and_A_notB[0], and_B_notA[0]);	
	nor #(4ns) nor2(x[1], and_A_notB[1], and_B_notA[1]);
	nor #(4ns) nor3(x[2], and_A_notB[2], and_B_notA[2]);
	nor #(4ns) nor4(x[3], and_A_notB[3], and_B_notA[3]);
	nor #(4ns) nor5(x[4], and_A_notB[4], and_B_notA[4]);
	nor #(4ns) nor6(x[5], and_A_notB[5], and_B_notA[5]);
	
	// for equality
	and #(6ns) andeq(A_equal_B, x[0], x[1], x[2], x[3], x[4], x[5]);
	
	//A < B
	and #(6ns) a13(y[4], x[5], and_B_notA[4]);
	and #(6ns) a14(y[3], x[5], x[4], and_B_notA[3]);
	and #(6ns) a15(y[2], x[5], x[4], x[3], and_B_notA[2]);
	and #(6ns) a16(y[1], x[5], x[4], x[3], x[2], and_B_notA[1]);
	and #(6ns) a17(y[0], x[5], x[4], x[3], x[2], x[1], and_B_notA[0]);
	
	or #(6ns) orls(A_smaller_B, and_B_notA[5], y[0], y[1], y[2], y[3], y[4]);
	
	//A > B
	and #(6ns) a18(z[4], x[5], and_A_notB[4]);
	and #(6ns) a19(z[3], x[5], x[4], and_A_notB[3]);
	and #(6ns) a20(z[2], x[5], x[4], x[3], and_A_notB[2]);
	and #(6ns) a21(z[1], x[5], x[4], x[3], x[2], and_A_notB[1]);
	and #(6ns) a22(z[0], x[5], x[4], x[3], x[2], x[1], and_A_notB[0]); 
	
	or #(6ns) orgt(A_greater_B, and_A_notB[5], z[0], z[1], z[2], z[3], z[4]);
	

endmodule	  



module five_bit_mag_comp(input [4:0] A, B,output A_greater_B, A_equal_B, A_smaller_B);

	wire [4:0] notA, notB;
	wire [4:0] and_A_notB, and_B_notA;	
	wire [4:0] x;

	wire [3:0] y;
	wire [3:0] z;
	// to get ~A and ~B
	not #(3ns) n1(notA[0], A[0]);
	not #(3ns) n2(notA[1], A[1]); 
	not #(3ns) n3(notA[2], A[2]);
	not #(3ns) n4(notA[3], A[3]);
	not #(3ns) n5(notA[4], A[4]);
	
	
	not #(3ns) n7(notB[0], B[0]);
	not #(3ns) n8(notB[1], B[1]); 
	not #(3ns) n9(notB[2], B[2]);
	not #(3ns) n10(notB[3], B[3]);
	not #(3ns) n11(notB[4], B[4]);
	
	
	// to do and gates

	and #(6ns) a3(and_B_notA[4], notA[4], B[4]);
	and #(6ns) a4(and_A_notB[4], notB[4], A[4]); 
	and #(6ns) a5(and_B_notA[3], notA[3], B[3]);
	and #(6ns) a6(and_A_notB[3], notB[3], A[3]); 
	and #(6ns) a7(and_B_notA[2], notA[2], B[2]);
	and #(6ns) a8(and_A_notB[2], notB[2], A[2]);
	and #(6ns) a9(and_B_notA[1], notA[1], B[1]);
	and #(6ns) a10(and_A_notB[1], notB[1], A[1]);
	and #(6ns) a11(and_B_notA[0], notA[0], B[0]);
	and #(6ns) a12(and_A_notB[0], notB[0], A[0]);  
	
	nor #(4ns) nor1(x[0], and_A_notB[0], and_B_notA[0]);	
	nor #(4ns) nor2(x[1], and_A_notB[1], and_B_notA[1]);
	nor #(4ns) nor3(x[2], and_A_notB[2], and_B_notA[2]);
	nor #(4ns) nor4(x[3], and_A_notB[3], and_B_notA[3]);
	nor #(4ns) nor5(x[4], and_A_notB[4], and_B_notA[4]);
	
	
	// for equality
	and #(6ns) andeq(A_equal_B, x[0], x[1], x[2], x[3], x[4]);
	
	//A < B
	and #(6ns) a14(y[3], x[4], and_B_notA[3]);
	and #(6ns) a15(y[2], x[4], x[3], and_B_notA[2]);
	and #(6ns) a16(y[1], x[4], x[3], x[2], and_B_notA[1]);
	and #(6ns) a17(y[0], x[4], x[3], x[2], x[1], and_B_notA[0]);
	
	or #(6ns) orls(A_smaller_B, and_B_notA[4], y[0], y[1], y[2], y[3]);
	
	//A > B
	
	and #(6ns) a19(z[3], x[4], and_A_notB[3]);
	and #(6ns) a20(z[2], x[4], x[3], and_A_notB[2]);
	and #(6ns) a21(z[1], x[4], x[3], x[2], and_A_notB[1]);
	and #(6ns) a22(z[0], x[4], x[3], x[2], x[1], and_A_notB[0]); 
	
	or #(6ns) orgt(A_greater_B, and_A_notB[4], z[0], z[1], z[2], z[3]);
	

endmodule


module signed_comp(input [5:0] A, B,output reg A_greater_B, A_equal_B, A_smaller_B);
	wire [4:0] A_mag, B_mag;
	wire msb_comparison, mag_less, mag_equal, mag_greater;
	
	
	
	assign A_mag = A[4:0];
	assign B_mag = B[4:0];
	
		
	
    //Compare magnitudes for same sign
	five_bit_mag_comp mag_comp(
		.A(A_mag),
		.B(B_mag),
		.A_greater_B(mag_greater),
		.A_equal_B(mag_equal),
		.A_smaller_B(mag_less)
	);
	
	// Combine results	
	wire A_sign, B_sign;
    wire not_A_sign, not_B_sign;
    wire A_eq_B, A_lt_B_by_sign, A_gt_B_by_sign;
	
	assign A_sign = A[5];
	assign B_sign = B[5];
    // NOT gates for a_sign and b_sign
    not #(3ns) u1(not_A_sign, A_sign);
    not #(3ns) u2(not_B_sign, B_sign);

    // a_sign == b_sign using XOR and NOT
    wire xor_signs;
    xor #(9ns) u3(xor_signs, A_sign, B_sign);  // XOR to check if signs are different
    not #(3ns) u4(A_eq_B, xor_signs);          // NOT of XOR gives equality

    // a < b by sign: a_sign & ~b_sign
    and #(6ns) u5(A_lt_B_by_sign, A_sign, not_B_sign);

    // a > b by sign: ~a_sign & b_sign
    and #(6ns) u6(A_gt_B_by_sign, not_A_sign, B_sign);

    // Combine for A_smaller_B: (a_sign & ~b_sign) | ((a_sign == b_sign) & mag_less)
    wire less_same_sign;
    and #(6ns) u7(less_same_sign, A_eq_B, mag_less);  // ((a_sign == b_sign) & mag_less)
    or #(6ns) u8(A_smaller_B, A_lt_B_by_sign, less_same_sign);

    // Combine for A_greater_B: (~a_sign & b_sign) | ((a_sign == b_sign) & mag_greater)
    wire greater_same_sign;
    and #(6ns) u9(greater_same_sign, A_eq_B, mag_greater);  // ((a_sign == b_sign) & mag_greater)
    or #(6ns) u10(A_greater_B, A_gt_B_by_sign, greater_same_sign);

    // Combine for A_equal_B: (a_sign == b_sign) & mag_equal
    and #(6ns) u11(A_equal_B, A_eq_B, mag_equal);
	
endmodule 


module mux(input x1,x2,s, output f);
	wire k,g,h;
	not #(3ns)(k,s);
	and #(6ns) n1(g,k,x1);
	and #(6ns) n2(h,s,x2);
	or #(6ns)(f,g,h);
endmodule

module register_6bit(
    input clock,
    input [5:0] A, 
    input [5:0] B,
	input Selection,
    output reg [5:0] A_out,
	output reg Selection_out,
    output reg [5:0] B_out
);
    always @(posedge clock) begin
        A_out <= A; // Store input A in output A_out
        B_out <= B; // Store input B in output B_out 
		Selection_out <= Selection;
    end
endmodule



// Module to handle the output of the comparator
module output_register(
    input clock,
    input A_greater_B,
    input A_equal_B,
    input A_smaller_B,
    output reg reg_A_greater_B,
    output reg reg_A_equal_B,
    output reg reg_A_smaller_B
);
    always @(posedge clock) begin
        reg_A_greater_B <= A_greater_B;
        reg_A_equal_B <= A_equal_B;
        reg_A_smaller_B <= A_smaller_B;
    end
endmodule

// Main module incorporating the new output register module
module main_module(
    input clock,
    input [5:0] A, B,
    input Selection,
    output A_greater_B,
    output A_smaller_B,
    output A_equal_B
);

    // Internal signals for input and output registers
    wire [5:0] regA, regB;				
	wire reg_selection;
    wire comp_A_greater_B, comp_A_smaller_B, comp_A_equal_B;
    wire reg_A_greater_B, reg_A_smaller_B, reg_A_equal_B;
	wire unsigned_A_greater_B, unsigned_A_equal_B, unsigned_A_smaller_B, signed_A_greater_B, signed_A_equal_B, signed_A_smaller_B;

    // 6-bit input register for A, B, and Selection
    register_6bit input_registers(
        .clock(clock),
        .A(A),
        .B(B),
        .Selection(Selection),
        .A_out(regA),
		.Selection_out(reg_selection),
        .B_out(regB)
    );

    // Unsigned comparator
    unsigned_comp unsigned_comparator(
        .A(regA),
        .B(regB),
        .A_greater_B(unsigned_A_greater_B),
        .A_equal_B(unsigned_A_equal_B),
        .A_smaller_B(unsigned_A_smaller_B)
    );

    // Signed comparator
    signed_comp signed_comparator(
        .A(regA),
        .B(regB),
        .A_greater_B(signed_A_greater_B),
        .A_equal_B(signed_A_equal_B),
        .A_smaller_B(signed_A_smaller_B)
    );

    // Select between unsigned and signed comparator based on `Selection`
    // MUX for comp_A_greater_B
	mux mux1(
	    .x1(unsigned_A_greater_B),
	    .x2(signed_A_greater_B),
	    .s(reg_selection),
	    .f(comp_A_greater_B)
	);
	
	// MUX for comp_A_smaller_B
	mux mux2(
	    .x1(unsigned_A_smaller_B),
	    .x2(signed_A_smaller_B),
	    .s(reg_selection),
	    .f(comp_A_smaller_B)
	);
	
	// MUX for comp_A_equal_B
	mux mux3(
	    .x1(unsigned_A_equal_B),
	    .x2(signed_A_equal_B),
	    .s(reg_selection),
	    .f(comp_A_equal_B)
	);


    // Output register for comparator results
    output_register output_registers(
        .clock(clock),
        .A_greater_B(comp_A_greater_B),
        .A_equal_B(comp_A_equal_B),
        .A_smaller_B(comp_A_smaller_B),
        .reg_A_greater_B(reg_A_greater_B),
        .reg_A_equal_B(reg_A_equal_B),
        .reg_A_smaller_B(reg_A_smaller_B)
    );

    // Assign final outputs
    assign A_greater_B = reg_A_greater_B;
    assign A_smaller_B = reg_A_smaller_B;
    assign A_equal_B = reg_A_equal_B;

endmodule

module testbench;

    // Declare inputs as reg and outputs as wire
    reg clock;
    reg [5:0] A, B;
    reg Selection;
    wire A_greater_B, A_smaller_B, A_equal_B;

    // Instantiate the main module
    main_module uut (
        .clock(clock),
        .A(A),
        .B(B),
        .Selection(Selection),
        .A_greater_B(A_greater_B),
        .A_smaller_B(A_smaller_B),
        .A_equal_B(A_equal_B)
    );

    // Instantiate the comparator module for verification
    wire ref_A_greater_B, ref_A_smaller_B, ref_A_equal_B;
    verification reference ( 
		.clk(clock),
        .A(A),
        .B(B),
        .Selection(Selection),
        .A_greater_B(ref_A_greater_B),
        .A_equal_B(ref_A_equal_B),
        .A_smaller_B(ref_A_smaller_B)
    );

    // Clock generation
    initial begin 
        clock = 0;
        forever #100ns clock = ~clock;  // Toggle clock every 100 time units
    end

    // Testbench logic
    integer error_count = 0;  // Error counter
    integer total_tests = 0; // Total test cases counter

    initial begin
        // Initialize signals
        A = 6'b000000;
        B = 6'b000000;
        Selection = 0;

        // Wait for some time to begin testing
        #110ns;

        // Generate all test cases
        repeat (2) begin  // Toggle Selection (unsigned and signed comparison)
            Selection = ~Selection;
            repeat (64) begin  // Iterate over all possible values of A
                A = A + 6'b000001;
                repeat (64) begin  // Iterate over all possible values of B
                    B = B + 6'b000001;
                    @(posedge clock);  // Wait for the clock edge

                    // Compare outputs and log errors
                    total_tests = total_tests + 1;
                    if ((A_greater_B !== ref_A_greater_B) ||
                        (A_smaller_B !== ref_A_smaller_B) ||
                        (A_equal_B !== ref_A_equal_B)) begin
                        error_count = error_count + 1;
                        $display("FAIL: A=%b, B=%b, Selection=%b | DUT: A_greater_B=%b, A_smaller_B=%b, A_equal_B=%b | REF: A_greater_B=%b, A_smaller_B=%b, A_equal_B=%b",
                                 A, B, Selection, A_greater_B, A_smaller_B, A_equal_B, ref_A_greater_B, ref_A_smaller_B, ref_A_equal_B);
                    end
                end
            end
        end

        // Print summary after all tests
        $display("Test Summary:");
        $display("Total Tests Run: %0d", total_tests);
        $display("Total Errors: %0d", error_count);
        if (error_count == 0) begin
            $display("Result: ALL TESTS PASSED!");
        end else begin
            $display("Result: TESTS FAILED.");
        end

        // End simulation
        $finish;
    end

endmodule


//build a behavioral comparartor to compare the results for verification
module verification(
    input [5:0] A,
    input [5:0] B,
    input Selection, // 0 for unsigned, 1 for signed
    input clk,       // Clock signal
    output reg A_greater_B,
    output reg A_equal_B,
    output reg A_smaller_B
);
    // Internal registers to store A and B
    reg [5:0] reg_A;
    reg [5:0] reg_B;

    always @(posedge clk) begin
        // Store inputs in registers
        reg_A <= A;
        reg_B <= B;

        // Perform comparison based on Selection
        if (Selection == 0) begin
            // Unsigned comparison
            A_greater_B <= (reg_A > reg_B);
            A_equal_B <= (reg_A == reg_B);
            A_smaller_B <= (reg_A < reg_B);
        end else begin
            // Signed comparison
            if ($signed(reg_A) > $signed(reg_B)) begin
                A_greater_B <= 1;
                A_equal_B <= 0;
                A_smaller_B <= 0;
            end else if ($signed(reg_A) == $signed(reg_B)) begin
                A_greater_B <= 0;
                A_equal_B <= 1;
                A_smaller_B <= 0;
            end else begin
                A_greater_B <= 0;
                A_equal_B <= 0;
                A_smaller_B <= 1;
            end
        end
    end
endmodule
