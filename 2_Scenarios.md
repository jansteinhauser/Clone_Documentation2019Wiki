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

The diet scenario determines the targeted average daily kilocalorie consumption per capita (kcal/cap/day) for each food group and each time step. Scenarios include IIASA-GLOBIOM SSP scenarios where future consumption levels depend on GDP per capita and income elasticities from USDA. Three other scenarios were defined in the Calculator by default: No change, Healthy diet, and Fat diet. No change corresponds to the 2010 consumption profile taken from the FAO. Healthy diet corresponds to an average of the range indicated by the [EAT-Lancet report](https://www.thelancet.com/pdfs/journals/lancet/PIIS0140-6736(18)31788-4.pdf?utm_campaign=tleat19&utm_source=HubPage) for each food group (Willett et al., 2019). We have defined the Fat Diet as a high share of meat products, oil, and sugar in the total food intake (Table 3). We compute the difference between the kilocalorie consumption per food group in the selected diet and the consumption level observed in 2010. This difference is then progressively reduced over time starting in 2015 in order to match the selected diet in 2050. Several implementation rates of the target can be chosen [(Appendix 2)](https://github.com/FableCalculator/DocumentationWiki/wiki/7_2-Appendix-2). Corresponding shifters are computed for each time step. The shifters are the same for all the products within a food group [(Appendix 1)](https://github.com/FableCalculator/DocumentationWiki/wiki/7_1-Appendix-1).

![Table 3](https://user-images.githubusercontent.com/68918893/88783960-bf67c980-d18f-11ea-878c-b96d3d891398.png)
![Table 3a](https://user-images.githubusercontent.com/68918893/88784225-1372ae00-d190-11ea-8db3-c78389986cd2.png)

## 2.4 Food waste

Food waste corresponds to the waste at the household level (i.e. excluding post-harvest losses which are included as a separate parameter in the FABLE Calculator). Food waste is represented as a share of total food consumption. For instance, if the targeted food consumption is 2500 kcal/cap/day, the total market supply needs to correspond to an average consumption level of 2750 kcal/cap/day if food waste at the household level represents 10% of consumption. A default share of 10% is applied to all food groups. Three scenarios are available: a constant share of food waste over time, increased food waste over time (up to 20% in 2050) and reduced food waste over time (down to 5% in 2050).

## 2.5 Trade

Imports are computed based on total consumption including food and non-food human consumption, food waste, and feed consumption. The parameter which allows the computation of future imports is the share of the total consumption which is satisfied by imports. Exports are computed differently: targeted exports are purely exogenous and expressed in 1000 tons. The final exports can be reduced if there is not enough land [(cf. Feasible production, trade and consumption)](https://github.com/FableCalculator/DocumentationWiki/wiki/3_5.-Feasible-production,-trade,-and-consumption). The default assumption is that the share of the total consumption which is imported, and the level of exports, remain constant at the 2010 level, as reported by the FAO in the Commodity Balances (FAOSTAT, 2019). The “Exports” and “Imports” scenarios make it possible to change this assumption but only for the products which are selected in the export and import scenarios tables (Tables product_impscen and product_exports; [Appendix 4](https://github.com/FableCalculator/DocumentationWiki/wiki/7_4-Appendix-4)). Users can specify by how much the 2010 exports or the 2010 share of consumption which is imported will vary by 2050 for each selected product using a shifter (2010=1) and the implementation rate of the target [(Appendix 2)](https://github.com/FableCalculator/DocumentationWiki/wiki/7_2-Appendix-2). By-default, three scenarios are defined for the imports (I1, I2, and I3) and 3 scenarios are defined for the exports (E1, E2, E3) with no change, reduced, and increased trade assumptions.

One scenario makes it possible to fix trade to certain values, (i.e. overwriting the previous imports and exports scenarios and impeding trade adjustment due to the land constraint (Fix Trade scenario). This scenario is used during the Scenathon for the global trade harmonisation stage after the global trade imbalance that is produced once the results of all country and regional Calculators have been computed and national and regional net trade have been adjusted accordingly.

## 2.6 Productivity

Because of the large number of products, the design of the scenarios on productivity relies on very simplistic assumptions: the starting point is always the historical productivity growth over 2000-2010 which is computed based on FAOSTAT Production data (FAOSTAT, 2019). The default assumption in the High productivity growth scenario is that the historical growth rate will be multiplied by -1 if it was negative, by 2 if it was below 1%, and by 0.7 if it was above 1%. For the Low productivity growth scenario, the historical growth rate is multiplied by -0.5 if the historical growth rate was negative, by 0.5 if it was lower than 1%, and by 0.1 if it was higher than 1%. Two additional alternative scenarios are available: NoChange which fixes the crop productivity to the 2010 level, and BAUGrowth which uses the same crop productivity growth as observed during 2000-2010. We have added a condition so that productivity cannot drop below 50% of the reported yield in 2010. In the future, we plan to add maximum productivity values to avoid unrealistic productivity projections. This is the priority for improving the tool.

## 2.7 Land availability

This scenario makes it possible to restrict agricultural expansion even when there is still some land available. There are three default scenarios: No expansion, which places a restriction on the expansion of agricultural land beyond 2010 agricultural land area; NoDefor2030, which forbids agricultural expansion on forest land after 2030; and Free expansion, which allows for agricultural expansion of natural land up to the limit of the natural land area which is under protection.

## 2.8 Afforestation/reforestation

Afforestation (or reforestation) is exogenously driven in the FABLE Calculator. Afforestation (or reforestation) is represented as a separate land cover class and this scenario fixes the total targeted afforested area by 2050 and the share of the total afforested area which is planned on each land cover type (i.e. cropland, pasture and other natural land) then selects the implementation rate to distribute the afforestation target over the period. There are two alternative scenarios: No afforestation and BonnChallenge, where the target should correspond to the commitments which have been made under the Bonn Challenge.

Additional scenarios are available in certain optional features of the Calculator [(cf. Appendix 5)](https://github.com/FableCalculator/DocumentationWiki/wiki/7_5-Appendix-5).

[Next Section: 3 Calculation Steps](https://github.com/FableCalculator/DocumentationWiki/wiki/3_0.-Calculation-Steps)

