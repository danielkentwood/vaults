# ç SQL get top N items per group
created:: 2022-08-31 05:16
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[HackerRank]]
***

- example problem #1
    
    [https://leetcode.com/problems/department-top-three-salaries/](https://leetcode.com/problems/department-top-three-salaries/)
    
    ![SQL%20get%20top%20N%20items%20per%20group%20ff350464dd824578bee9e274df7c527c/Untitled.png](Untitled%2020.png)
    
    - example solution #1
        
        ```sql
        select t1.dept_name Department, t1.emp_name Employee, t1.Salary
        from (select t2.dept_name, t2.emp_name, t2.Salary, 
              dense_rank() over (partition by t2.DepartmentID order by t2.Salary desc) drank
              from (select e.DepartmentID, e.Salary, e.Name emp_name, d.Name dept_name
                    from Employee e
                    inner join Department d
                    on d.Id = e.DepartmentId) t2) t1
        where t1.drank < 4
        ```
        
- example problem #2
    
    Out of all cities, find the top 3 cities in each country by population
    
    - example solution #2
        
        ```sql
        select * from (
            select country, 
                   city,
                   population, 
                   row_number() over (partition by country order by population desc) as country_rank 
            from cities) ranks
        where country_rank <= 2;
        ```
        
- Approach
    
    The best way to solve this type of problem is to use a window function.
    
    - r**ow_number()** assigns a number to each individual row.
    - **dense_rank()** assigns a rank to each unique distinct rank value (i.e., you can have rows with the same rank if their values are equal). The rankings are consecutive.
    - **rank()** is the same as dense_rank(), but if there is a tie, the ranking skips according to the number of ties (e.g., if there is a three-way tie for 2nd place, the next rank will be 5th place)
    
    For all of these, you do the following:
    
    1. dense_rank() over
    2. partition by <expression>
    3. order by <expression> [ASC | DESC]
    
    One important note is that these window functions are typically the last step (e.g., after joins). Otherwise, the ranking might get messed up.
    
- resources
    - [http://www.silota.com/docs/recipes/sql-top-n-group.html](http://www.silota.com/docs/recipes/sql-top-n-group.html)