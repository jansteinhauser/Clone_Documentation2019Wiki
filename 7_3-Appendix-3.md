# Appendix 3: Guidelines to use the FABLE Calculator

## Conventions of the FABLE Calculator


![Appendix 3](https://user-images.githubusercontent.com/68918893/88806475-c3581380-d1b0-11ea-9c23-f2df3afe4d68.png)

![Appendix 3a](https://user-images.githubusercontent.com/68918893/88806753-1df16f80-d1b1-11ea-8403-4a790f9c3c70.png)

## Most used Excel features and formulas

Each table is formatted as a table i.e. when you create a new table you have to select the table and click on "Format as a table" (cf. Figure A3.4). This is a nice feature in Excel which:
- gives a name to a table which can be directly used in calculations,
- recognizes automatically all columns’ names which can be used in calculations as an attribute of the table name,
- the calculation entered in the first row is automatically copied to all the lines of the table in the same column.
There are several advantages of using this feature. It allows some kind of programming language in the formulas and it is easier to understand the formula when table names are self-explanatory. There is some tradeoff here between the length of a table name and the name being self-explanatory as a long table name will also increase the length of a formula and a long formula is harder to understand.

![Appendix 3b](https://user-images.githubusercontent.com/68918893/88807156-a4a64c80-d1b1-11ea-8c25-9831c43e370b.png)

For instance, if you click on the cell AA28 in the worksheet 1_calc_hum_demand you see that the value of this cell is equal to the column "Pop_shift"of the table called "gdp_pop_hist" when the year is lower or equal than 2015, and to the column "pop_shift_2000" from the table GdpPopTarget when the year is higher than 2015 :
=IF([@year]<=2015,SUMIF(gdp_pop_hist[YEAR],[@year],gdp_pop_hist[POP_shift]),SUMIFS(GdpPopTarget[POP_shift_2000],GdpPopTarget[SCEN],[@[POP_scen]],GdpPopTarget[YEAR],[@year]))

You can easily find the table called gdp_pop_hist if you do an advanced search in the whole workbook looking for gdp_pop_hist in values. You will be directed to the cell where the name gdp_pop_hist appears which is at the top of the worksheet where the table is introduced, and above the table. Or you can go to the worksheet Index Tables and look for the table name in the first column. If you click on it, you will be also directed to the table.

The most used formulas in the FABLE Calculator are:

- IF - e.g. in the table called calc_hum_demand, in the column popshift (calc_hum_demand[popshift]).
- IFERROR - e.g. in calc_crops[PlantArea]
- AND - e.g. in calc_livestocknb[FinalExports]
- SUMIF - e.g. in calc_hum_demand[popshift])
- SUMIFS - e.g. in calc_hum_demand[popshift])
- VLOOKUP - e.g. in calc_crops[Crop_scen]
- OFFSET - e.g. in calc_land_cor[Initpasture]

We encourage users who are not yet familiar with these formulas to look at the help within Excel and explanations in several forums and online Excel tutorials.

![Appendix 3c](https://user-images.githubusercontent.com/68918893/88807285-d4555480-d1b1-11ea-8eb0-2a98d1bae209.png)

## Documentation of the changes

It is good practice to document your changes in the Change Log worksheet: it is useful for the user itself because we tend to forget quickly, especially if we carry several projects at the same time, and when different people work on the same tool. We recommend that the FABLE Calculator is saved under different version names after a change or a series of changes are implemented.
