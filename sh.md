

SELECT  QURContestants.Name as ContestantName,
		Dusers.UserNameAr as JudgeName,
		QUREvaluationQuestions.TotalQuestionScore,
		QUREvaluationQuestions.Comment
	
FROM QUREvaluationQuestions
inner join QURContestants on QURContestants.ID = QUREvaluationQuestions.ContestantID
inner join Dusers on DUsers.UserID = QUREvaluationQuestions.Judge
where CyclePhaseID = 40



select 
		RegistrationUserID,
		Name,
		(select NationalityAr from QURNationalities where QURNationalities.ID = QURContestants.Nationality) as Nationality,
		(select GenderAr from QURGenders where QURGenders.ID = QURContestants.Gender) as Gender,
		CAST(DateOfBirth AS date) as DateOfBirth,
		 (
        YEAR(GETDATE())
        - YEAR(QURContestants.DateOfBirth)
        - CASE
            WHEN DATEFROMPARTS(YEAR(GETDATE()), 5, 31)
                 <
                 DATEFROMPARTS(
                     YEAR(GETDATE()),
                     MONTH(QURContestants.DateOfBirth),
                     IIF(DAY(QURContestants.DateOfBirth) 
                           > DAY(EOMONTH(DATEFROMPARTS(YEAR(GETDATE()), MONTH(QURContestants.DateOfBirth), 1))),
                         DAY(EOMONTH(DATEFROMPARTS(YEAR(GETDATE()), MONTH(QURContestants.DateOfBirth), 1))),
                         DAY(QURContestants.DateOfBirth))
                 )
            THEN 1
            ELSE 0
          END
    ) AS Age,
		Email,
		ContactNumber,
		TotalPhaseGrade


from QURPhaseContestants
inner join QURContestants on QURContestants.ID =  QURPhaseContestants.Contestant
where CyclePhase = 40
