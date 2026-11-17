<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Student Portal</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <nav class="navbar navbar-expand-lg bg-dark" data-bs-theme="dark">
    <div class="container">
      <a class="navbar-brand" href="#dashboard">Student Portal</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#mainNav" aria-controls="mainNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="mainNav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item"><a class="nav-link" href="#dashboard">Home</a></li>
          <li class="nav-item"><a class="nav-link" href="#dashboard">Subjects</a></li>
          <li class="nav-item"><a class="nav-link" href="#register">Register</a></li>
        </ul>
      </div>
    </div>
  </nav>

  <div class="container py-4">
    <h1 class="text-center mb-4" id="dashboard">Dashboard</h1>

    <div class="row g-3">
      <div class="col-12 col-sm-6 col-lg-4">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">Profile</h5>
            <p class="card-text" id="profileText">No profile yet. Register first.</p>
            <a href="#" class="btn btn-primary card-btn" data-type="profile">Open</a>
          </div>
        </div>
      </div>

      <div class="col-12 col-sm-6 col-lg-4">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">Announcements</h5>
            <p class="card-text" id="announceText">Register to see your announcements.</p>
            <a href="#" class="btn btn-primary card-btn" data-type="announcements">Read</a>
          </div>
        </div>
      </div>

      <div class="col-12 col-sm-6 col-lg-4">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">Subjects</h5>
            <p class="card-text" id="subjectsText">Register to see your subjects.</p>
            <a href="#" class="btn btn-primary card-btn" data-type="subjects">View</a>
          </div>
        </div>
      </div>
    </div>

    <h2 class="mt-5 mb-3" id="register">Register</h2>

    <div id="message"></div>

    <form class="row g-3" id="registerForm" novalidate>
      <div class="col-12 col-md-6">
        <label for="name" class="form-label">Name</label>
        <input type="text" class="form-control" id="name">
        <div class="invalid-feedback">Please enter your name.</div>
      </div>
      <div class="col-12 col-md-6">
        <label for="email" class="form-label">Email</label>
        <input type="email" class="form-control" id="email">
        <div class="invalid-feedback">Please enter a valid email.</div>
      </div>
      <div class="col-12 col-md-6">
        <label for="program" class="form-label">Program</label>
        <select class="form-select" id="program">
          <option value="BSIS">BSIS</option>
          <option value="BSIT">BSIT</option>
          <option value="BSCS">BSCS</option>
        </select>
      </div>
      <div class="col-12">
        <button type="submit" class="btn btn-primary">Submit</button>
      </div>
    </form>

    <div class="table-responsive mt-4 d-none" id="tableBox">
      <table class="table table-striped align-middle">
        <thead>
          <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Program</th>
            <th></th>
          </tr>
        </thead>
        <tbody id="studentList"></tbody>
      </table>
    </div>
  </div>

  <div class="modal fade" id="infoModal" tabindex="-1" aria-labelledby="modalTitle" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="modalTitle"></h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body" id="modalText" style="white-space: pre-line;"></div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <script>
    $(function () {
      const subjectsByProgram = {
        BSIS: ['Systems Analysis and Design', 'Web Development', 'Database Management', 'IT Project Management'],
        BSIT: ['Network Administration', 'Web Development', 'Database Management', 'Systems Integration'],
        BSCS: ['Data Structures and Algorithms', 'Web Development', 'Discrete Mathematics', 'Operating Systems']
      };

      const students = [];
      let current = null;

      function getAnnouncements(student) {
        return [
          'Enrollment ends this Friday.',
          'Orientation for ' + student.program + ' students is on Monday at 9:00 AM.',
          'Please check your subjects for this semester.'
        ];
      }

      function showMessage(text, type) {
        const alertBox = $('<div class="alert alert-dismissible fade show"></div>')
          .addClass('alert-' + type)
          .text(text);

        alertBox.append('<button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>');
        $('#message').empty().append(alertBox);
      }

      function setState(input, isValid) {
        input.toggleClass('is-valid', isValid).toggleClass('is-invalid', !isValid);
      }

      function updateCards() {
        if (current === null) {
          $('#profileText').text('No profile yet. Register first.');
          $('#announceText').text('Register to see your announcements.');
          $('#subjectsText').text('Register to see your subjects.');
          return;
        }

        const student = students[current];
        $('#profileText').text('Welcome, ' + student.name + ' (' + student.program + ').');
        $('#announceText').text(getAnnouncements(student).length + ' announcements for ' + student.name + '.');
        $('#subjectsText').text(subjectsByProgram[student.program].length + ' subjects enrolled.');
      }

      function renderTable() {
        $('#studentList').empty();

        $.each(students, function (index, student) {
          const row = $('<tr></tr>');

          row.append($('<td></td>').text(student.name));
          row.append($('<td></td>').text(student.email));
          row.append($('<td></td>').text(student.program));
          row.append(
            '<td class="text-end text-nowrap">' +
            '<button class="btn btn-sm btn-outline-primary me-1 view-btn" data-index="' + index + '">View</button>' +
            '<button class="btn btn-sm btn-outline-danger remove-btn" data-index="' + index + '">Remove</button>' +
            '</td>'
          );

          if (index === current) {
            row.addClass('table-primary');
          }

          $('#studentList').append(row);
        });

        $('#tableBox').toggleClass('d-none', students.length === 0);
      }

      function refresh() {
        renderTable();
        updateCards();
      }

      function showInfo(type) {
        let title = '';
        let text = '';

        if (current === null) {
          title = 'Nothing yet';
          text = 'Please register first.';
        } else {
          const student = students[current];

          if (type === 'profile') {
            title = 'Profile';
            text = 'Name: ' + student.name + '\nEmail: ' + student.email + '\nProgram: ' + student.program;
          } else if (type === 'announcements') {
            title = 'Announcements';
            text = $.map(getAnnouncements(student), function (item) {
              return '• ' + item;
            }).join('\n');
          } else {
            title = 'Subjects';
            text = $.map(subjectsByProgram[student.program], function (item) {
              return '• ' + item;
            }).join('\n');
          }
        }

        $('#modalTitle').text(title);
        $('#modalText').text(text);

        if (typeof bootstrap === 'undefined') {
          alert(title + '\n\n' + text);
          return;
        }

        bootstrap.Modal.getOrCreateInstance($('#infoModal')[0]).show();
      }

      $('#registerForm').on('submit', function (e) {
        e.preventDefault();

        const nameInput = $('#name');
        const emailInput = $('#email');
        const name = $.trim(nameInput.val());
        const email = $.trim(emailInput.val());
        const nameOk = name.length >= 2;
        const emailOk = email !== '' && emailInput[0].checkValidity();

        setState(nameInput, nameOk);
        setState(emailInput, emailOk);

        if (!nameOk || !emailOk) {
          showMessage('Please fix the errors below.', 'danger');
          return;
        }

        const exists = students.some(function (student) {
          return student.email.toLowerCase() === email.toLowerCase();
        });

        if (exists) {
          showMessage('That email is already registered.', 'warning');
          return;
        }

        students.push({ name: name, email: email, program: $('#program').val() });
        current = students.length - 1;

        refresh();
        showMessage(name + ' was registered. Profile, announcements and subjects are ready.', 'success');
        this.reset();
        nameInput.removeClass('is-valid is-invalid');
        emailInput.removeClass('is-valid is-invalid');
      });

      $('#studentList').on('click', '.view-btn', function () {
        current = Number($(this).data('index'));
        refresh();
        showMessage('Now showing ' + students[current].name + '.', 'info');
      });

      $('#studentList').on('click', '.remove-btn', function () {
        students.splice(Number($(this).data('index')), 1);
        current = students.length > 0 ? students.length - 1 : null;
        refresh();
      });

      $('.card-btn').on('click', function (e) {
        e.preventDefault();
        showInfo($(this).data('type'));
      });

      $('.nav-link').on('click', function () {
        if (typeof bootstrap !== 'undefined') {
          bootstrap.Collapse.getOrCreateInstance($('#mainNav')[0], { toggle: false }).hide();
        }
      });
    });
  </script>
</body>
</html>
