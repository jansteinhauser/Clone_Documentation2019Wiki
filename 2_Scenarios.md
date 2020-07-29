# 2 Scenarios
_Worksheet(s) in the FABLE Calculator:_

_⇒ Scenarios Selection_

_⇒ Scenarios Definition_

We have established a list of parameters that can be changed through the selection of different scenarios. Each parameter and corresponding alternative scenarios are grouped by tables. By default, there are 10 parameters which can be modified through scenarios, each of which has between 2 to 14 possible alternative values. There are, therefore, thousands of possible combinations that lead to different pathways (Table 1). The user can select pre-defined scenarios or add new scenarios. To select a scenario, the user simply needs to enter "x" next to the scenario that they want to test (Table 2). There can be only one scenario selected per table. The parameters and selected scenarios are automatically updated by the SUMIFS and VLOOKUP Excel functions, respectively.

![Table 1](https://user-images.githubusercontent.com/68918893/88782978-8549f800-d18e-11ea-92c0-2ddde3166ab9.png)

![Table 2](https://user-images.githubusercontent.com/68918893/88783113-b296a600-d18e-11ea-99dc-0b2a2ad6ce29.png)

A key concept for implementing the scenarios are shifters, which are created to introduce a time variation for any parameter based on historical value or trajectory.

## 2.1 Population

Population growth is a key parameter as it is used to compute the evolution of the targeted demand together with the diet assumption. Nine population projections are taken from the [United Nations DESA population division prospects](https://population.un.org/wpp/DataQuery/): low, medium, high, constant fertility, instant replacement, momentum, zero migration, constant mortality and no change (UNDESA, 2017). Five population projections are taken from the [SSP database](https://tntcat.iiasa.ac.at/SspDb/dsd?Action=htmlpage&page=10) developed at IIASA: SSP1 to SSP5 (KC & Lutz, 2017). Historical data for 2000, 2005, 2010, and 2015 are taken from UN-DESA (UNDESA, 2017). Shifters are computed as the ratio between the projected population in each time step and the population reported in 2015 in each database. The corresponding relative changes (shifters) to the selected population scenario are applied to the 2015 historical population level from the UN-DESA. It is important to note that the historical population value for 2015 is inconsistent across the UN and SSP databases.

## 2.2 GDP

GDP is only used in case the selected diet scenario is an SSP scenario. In this case, dietary evolution depends on the evolution of GDP per capita and the income elasticity of each food group. There are 3 alternative GDP projections taken from the IIASA-SSP database: SSP1 to SSP3 (Riahi et al., 2017).

## 2.3 Diets

The diet scenario determines the targeted average daily kilocalorie consumption per capita (kcal/cap/day) for each food group and each time step. Scenarios include IIASA-GLOBIOM SSP scenarios where future consumption levels depend on GDP per capita and income elasticities from USDA. Three other scenarios were defined in the Calculator by default: No change, Healthy diet, and Fat diet. No change corresponds to the 2010 consumption profile taken from the FAO. Healthy diet corresponds to an average of the range indicated by the [EAT-Lancet report](https://www.thelancet.com/pdfs/journals/lancet/PIIS0140-6736(18)31788-4.pdf?utm_campaign=tleat19&utm_source=HubPage) for each food group (Willett et al., 2019). We have defined the Fat Diet as a high share of meat products, oil, and sugar in the total food intake (Table 3). We compute the difference between the kilocalorie consumption per food group in the selected diet and the consumption level observed in 2010. This difference is then progressively reduced over time starting in 2015 in order to match the selected diet in 2050. Several implementation rates of the target can be chosen (Appendix 2). Corresponding shifters are computed for each time step. The shifters are the same for all the products within a food group (Appendix 1).

![Table 3](https://user-images.githubusercontent.com/68918893/88783960-bf67c980-d18f-11ea-878c-b96d3d891398.png)


