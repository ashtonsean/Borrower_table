CREATE TABLE borrowers_record (
    book_id INT NOT NULL,
    std_school_ID_number INT NOT NULL,
    std_id_number INT NOT NULL,
    staff_id INT NOT NULL,
    num_of_copies INT DEFAULT 1,
    release_date DATE NOT NULL,
    due_date DATE NOT NULL,

    -- Establishing Relationships
    FOREIGN KEY (book_id) REFERENCES library_books(book_id),
    FOREIGN KEY (std_id) REFERENCES student_list(std_id_number),
    FOREIGN KEY (staff_id) REFERENCES tbl_staff_list(staff_id) );

-- Insert a sample record: Student 'Adrian' borrows 'Clean Code' from Staff 'Beatrix'
INSERT INTO borrowers_record 
(book_id, std_id, staff_id, num_of_copies, release_date, due_date)
VALUES (7, 1, 1, 1, '2025-12-01', '2025-12-08');


SELECT
    br.borrower_record_id AS "Record ID",
    b.title AS "Book Title",
    s.std_name AS "Student Name",
    st.staff_first_name AS "Handled By",
    br.num_of_copies AS "Copies",
    br.release_date AS "Date Borrowed",
    br.due_date AS "Return Deadline" -- <-- NOTE: NO COMMA HERE
FROM 
    borrowers_record br
JOIN 
    library_books b ON br.book_id = b.book_id
JOIN 
    student_list s ON br.std_id = s.std_id_number
JOIN 
    tbl_staff_list st ON br.staff_id = st.staff_id; -- <-- ADDED SEMICOLON HERE
    
