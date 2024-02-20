### Broken

```sql ingestion_system
select distinct
    ingestion_system
from csv_data.ingestion_system_type_statistics
```

<Dropdown data={ingestion_system} name=ingestion_system value=ingestion_system>
    <DropdownOption value="%" valueLabel="All Agent Types"/>
</Dropdown>

```sql agent_counts
SELECT 
    *,
    --Format date as string because chart groups by millisecound otherwise
    strftime(date,'%Y-%m-%d') as date_str,
FROM csv_data.ingestion_system_type_statistics
where date BETWEEN CURRENT_DATE - INTERVAL 1 MONTH AND CURRENT_DATE
and  ingestion_system like '${inputs.ingestion_system}'
```

<BarChart 
    data={agent_counts} 
    x=date_str 
    y=shop_count
    series=ingestion_system
    title="Agent Distribution By Shop Count",
>
 <ReferenceLine x='2023-10-18' label="Batch #3 done" hideValue=true/>
</BarChart>