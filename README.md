# tecintenet_escola_eduardo
Banco de dados exercicío

## Fazendo CRUD 
```sql
INSERT INTO cursos(titulo,CargaHoraria) 
VALUES(
    'Front-End',
    40
),
(
    'Back-End',
    80
),(
    'UX,UI Design',
    30
),(
    'Figma',
    10
),(
    'Redes de computadores',
    100
);

INSERT INTO professores(nome,AreaAtuacao,Cursos_id )
VALUES(
    'Jon oliva',
    'área infra',
    5
), (
    'Lemmy kilmister',
    'área Design',
    4
),(
    'Neil peart',
    'área Design',
    3
),(
    'Ozzy osbourne',
    'área desenvolvimento',
    2
),(
    'David gilmour',
    'área desenvolvimento',
    1
);

INSERT INTO alunos(nome,DataNascimento,PrimeiraNota,SegundaNota,Cursos_id)
VALUES
  ('Alex', '2000-03-21', 9.00, 7.00, 1),
    ('Ben', '2001-05-15', 8.50, 9.00, 2),
    ('Cathy', '1999-11-03', 7.20, 8.00, 3),
    ('David', '2002-02-08', 6.80, 6.50, 4),
    ('Eva', '2003-07-20', 9.50, 9.80, 5),
    ('Frank', '2000-12-10', 8.00, 7.50, 1),
    ('Grace', '2001-09-25', 7.70, 8.70, 2),
    ('Helen', '1998-04-14', 6.00, 5.50, 3),
    ('Ivan', '2002-08-30', 9.20, 9.40, 4);

```

### Exercícios CRUD - Consultas

1. Faça uma consulta que mostre os alunos que nasceram antes do ano 2009
```sql
SELECT DataNascimento FROM alunos WHERE YEAR(DataNascimento) < 2009;
```

2. Faça uma consulta que calcule a média das notas de cada aluno e as mostre com duas casas decimais.
```sql
SELECT alunos.nome as Aluno,
       SUM(alunos.PrimeiraNota) as Nota1,
       SUM(alunos.SegundaNota) as Nota2,
       ROUND((SUM(alunos.PrimeiraNota) + SUM(alunos.SegundaNota)) / 2, 2) as Media
FROM alunos
GROUP BY alunos.nome;
```
3. Faça uma consulta que calcule o limite de faltas de cada curso de acordo com a carga horária. Considere o limite como 25% da carga horária. Classifique em ordem crescente pelo título do curso.

```sql
SELECT CargaHoraria,SUM(cursos.CargaHoraria * 0.25) FROM cursos
GROUP BY cursos.CargaHoraria;
```

4. Faça uma consulta que mostre os nomes dos professores que são somente da área "desenvolvimento".

```sql
SELECT nome,AreaAtuacao FROM professores WHERE AreaAtuacao = "Desenvolvimento";  
```

5. Faça uma consulta que mostre a quantidade de professores que cada área ("design", "infra", "desenvolvimento") possui.

```sql
SELECT nome,AreaAtuacao,COUNT(*) FROM professores WHERE AreaAtuacao IN ('Desenvolvimento', 'Infra', 'Design')
GROUP BY AreaAtuacao;
```

6. Faça uma consulta que mostre o nome dos alunos, o título e a carga horária dos cursos que fazem.

```sql
SELECT alunos.nome,cursos.titulo, cursos.CargaHoraria
FROM alunos INNER JOIN cursos ON alunos.Cursos_id = cursos.id;
```
7. Faça uma consulta que mostre o nome dos professores e o título do curso que lecionam. Classifique pelo nome do professor.

```sql
SELECT professores.nome,cursos.titulo FROM professores INNER JOIN cursos ON professores.Cursos_id = cursos.id
GROUP BY professores.nome;
```

8. Faça uma consulta que mostre o nome dos alunos, o título dos cursos que fazem, e o professor de cada curso.
```sql
SELECT alunos.nome,cursos.titulo,professores.nome as 'Professor'
FROM alunos INNER JOIN cursos ON alunos.Cursos_id = cursos.id 
INNER JOIN professores ON professores.Cursos_id = cursos.id;
```

9. Faça uma consulta que mostre a quantidade de alunos que cada curso possui. Classifique os resultados em ordem descrecente de acordo com a quantidade de alunos.

```sql
SELECT cursos.titulo as 'Título',COUNT(*) as 'Alunos' FROM cursos
LEFT JOIN alunos ON cursos.id = alunos.Cursos_id
GROUP BY cursos.id
ORDER BY 'Alunos' DESC;
```

10. Faça uma consulta que mostre o nome dos alunos, suas notas, médias, e o título dos cursos que fazem. Devem ser considerados somente os alunos de Front-End e Back-End. Mostre os resultados classificados pelo nome do aluno.

```sql
SELECT alunos.nome,alunos.PrimeiraNota,alunos.SegundaNota,
ROUND((SUM(alunos.PrimeiraNota) + SUM(alunos.SegundaNota)) / 2, 2) as Media,cursos.titulo
FROM alunos INNER JOIN cursos ON alunos.Cursos_id = cursos.id
WHERE cursos.titulo LIKE '%Back_End%' OR cursos.titulo LIKE '%Front-End%'
GROUP BY alunos.nome;
```

11. Faça uma consulta que altere o nome do curso de Figma para Adobe XD e sua carga horária de 10 para 15.

```sql
UPDATE cursos SET titulo = "Adobe XD",CargaHoraria = 15 WHERE id = 4;
```

12. Faça uma consulta que exclua um aluno do curso de Redes de Computadores e um aluno do curso de UX/UI.

```sql
DELETE FROM alunos WHERE id = 5 AND Cursos_id = 5;
DELETE FROM alunos WHERE id = 3 AND Cursos_id = 3;
```

13. Faça uma consulta que mostre a lista de alunos atualizada e o título dos cursos que fazem, classificados pelo nome do aluno.

```sql
SELECT alunos.nome as Alunos,cursos.titulo as Curso
FROM alunos INNER JOIN cursos ON alunos.Cursos_id = cursos.id
GROUP BY alunos.nome;
```
###