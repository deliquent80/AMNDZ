<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Student Portal</title>
  <style>

    :root {
      --blue: #0d6efd;
      --blue-hover: #0b5ed7;
      --blue-active: #0a58ca;
      --gray: #6c757d;
      --gray-hover: #5c636a;
      --gray-active: #565e64;
      --danger: #dc3545;
      --danger-hover: #bb2d3b;
      --danger-active: #b02a37;

      --body-color: #212529;
      --body-bg: #fff;
      --secondary-color: rgba(33, 37, 41, 0.75);
      --tertiary-bg: #f8f9fa;
      --border-color: #dee2e6;
      --border-translucent: rgba(0, 0, 0, 0.175);

      --radius: 0.375rem;
      --radius-sm: 0.25rem;
      --radius-lg: 0.5rem;

      --font: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", "Noto Sans",
              "Liberation Sans", Arial, sans-serif;
    }

    *,
    *::before,
    *::after {
      box-sizing: border-box;
    }

    html {
      -webkit-text-size-adjust: 100%;
    }

    body {
      margin: 0;
      font-family: var(--font);
      font-size: 1rem;
      font-weight: 400;
      line-height: 1.5;
      color: var(--body-color);
      background-color: var(--body-bg);
      -webkit-font-smoothing: antialiased;
    }

    h1, h2, h3, h4, h5, h6 {
      margin-top: 0;
      margin-bottom: 0.5rem;
      font-weight: 500;
      line-height: 1.2;
    }

    h1 { font-size: calc(1.375rem + 1.5vw); }
    h2 { font-size: calc(1.325rem + 0.9vw); }
    h5 { font-size: 1.25rem; }

    @media (min-width: 1200px) {
      h1 { font-size: 2.5rem; }
      h2 { font-size: 2rem; }
    }

    p { margin-top: 0; margin-bottom: 1rem; }
    ul { margin: 0; padding: 0; list-style: none; }
    a { color: var(--blue); text-decoration: underline; }
    a:hover { color: var(--blue-active); }
    img, svg { vertical-align: middle; }

    :focus-visible {
      outline: 0;
      box-shadow: 0 0 0 0.25rem rgba(13, 110, 253, 0.25);
    }

    .container {
      width: 100%;
      margin-inline: auto;
      padding-inline: 0.75rem;
    }

    @media (min-width: 576px)  { .container { max-width: 540px; } }
    @media (min-width: 768px)  { .container { max-width: 720px; } }
    @media (min-width: 992px)  { .container { max-width: 960px; } }
    @media (min-width: 1200px) { .container { max-width: 1140px; } }

    .row {
      --gx: 1.5rem;
      --gy: 0;
      display: flex;
      flex-wrap: wrap;
      margin-top: calc(-1 * var(--gy));
      margin-inline: calc(-0.5 * var(--gx));
    }

    .row > * {
      flex-shrink: 0;
      width: 100%;
      max-width: 100%;
      padding-inline: calc(0.5 * var(--gx));
      margin-top: var(--gy);
    }

    .g-3 { --gx: 1rem; --gy: 1rem; }

    .col-12 { flex: 0 0 auto; width: 100%; }

    @media (min-width: 576px) { .col-sm-6 { flex: 0 0 auto; width: 50%; } }
    @media (min-width: 768px) { .col-md-6 { flex: 0 0 auto; width: 50%; } }
    @media (min-width: 992px) { .col-lg-4 { flex: 0 0 auto; width: 33.33333333%; } }

    .d-none       { display: none !important; }
    .h-100        { height: 100% !important; }
    .text-center  { text-align: center !important; }
    .align-middle { vertical-align: middle !important; }
    .ms-auto      { margin-left: auto !important; }
    .py-4         { padding-block: 1.5rem !important; }
    .mb-3         { margin-bottom: 1rem !important; }
    .mb-4         { margin-bottom: 1.5rem !important; }
    .mt-4         { margin-top: 1.5rem !important; }
    .mt-5         { margin-top: 3rem !important; }

    .navbar {
      position: relative;
      padding: 0.5rem 0;
      color: rgba(255, 255, 255, 0.55);
    }

    .bg-dark { background-color: #212529; }

    .navbar > .container {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
    }

    .navbar-brand {
      margin-right: 1rem;
      padding-block: 0.3125rem;
      font-size: 1.25rem;
      line-height: inherit;
      white-space: nowrap;
      color: #fff;
      text-decoration: none;
    }

    .navbar-brand:hover { color: #fff; }

    .navbar-collapse {
      flex-basis: 100%;
      flex-grow: 1;
      align-items: center;
    }

    .navbar-nav {
      display: flex;
      flex-direction: column;
    }

    .nav-link {
      display: block;
      padding: 0.5rem 0;
      color: rgba(255, 255, 255, 0.55);
      text-decoration: none;
      transition: color 0.15s ease-in-out;
    }

    .nav-link:hover,
    .nav-link:focus { color: rgba(255, 255, 255, 0.75); }

    .navbar-toggler {
      padding: 0.25rem 0.75rem;
      font-size: 1.25rem;
      line-height: 1;
      color: rgba(255, 255, 255, 0.55);
      background: transparent;
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: var(--radius);
      cursor: pointer;
      transition: box-shadow 0.15s ease-in-out;
    }

    .navbar-toggler:focus { box-shadow: 0 0 0 0.25rem; outline: 0; }

    .navbar-toggler-icon {
      display: inline-block;
      width: 1.5em;
      height: 1.5em;
      vertical-align: middle;
      background: no-repeat center / 100%
        url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3e%3cpath stroke='rgba%28255, 255, 255, 0.75%29' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e");
    }

    @media (min-width: 992px) {
      .navbar-collapse {
        display: flex !important;
        flex-basis: auto;
      }

      .navbar-nav { flex-direction: row; }
      .nav-link { padding-inline: 0.5rem; }
      .navbar-toggler { display: none; }
    }

    .collapse:not(.show) { display: none; }

    .collapsing {
      height: 0;
      overflow: hidden;
      transition: height 0.35s ease;
    }

    .card {
      position: relative;
      display: flex;
      flex-direction: column;
      min-width: 0;
      background-color: var(--body-bg);
      border: 1px solid var(--border-translucent);
      border-radius: var(--radius);
    }

    .card-body {
      flex: 1 1 auto;
      padding: 1rem;
    }

    .card-title { margin-bottom: 0.5rem; }
    .card-text:last-child { margin-bottom: 0; }

    #registerForm { margin-top: 0; }

    .btn {
      display: inline-block;
      padding: 0.375rem 0.75rem;
      font-family: inherit;
      font-size: 1rem;
      font-weight: 400;
      line-height: 1.5;
      text-align: center;
      text-decoration: none;
      vertical-align: middle;
      color: var(--body-color);
      background-color: transparent;
      border: 1px solid transparent;
      border-radius: var(--radius);
      cursor: pointer;
      user-select: none;
      transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
                  border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
    }

    .btn:disabled { opacity: 0.65; pointer-events: none; }

    .btn:focus-visible {
      outline: 0;
      box-shadow: 0 0 0 0.25rem rgba(var(--ring, 49, 132, 253), 0.5);
    }

    .btn-sm {
      padding: 0.25rem 0.5rem;
      font-size: 0.875rem;
      border-radius: var(--radius-sm);
    }

    .btn-primary { color: #fff; background-color: var(--blue); border-color: var(--blue); }
    .btn-primary:hover { color: #fff; background-color: var(--blue-hover); border-color: var(--blue-active); }
    .btn-primary:active { color: #fff; background-color: var(--blue-active); border-color: #0a53be; }

    .btn-secondary { --ring: 130, 138, 145; color: #fff; background-color: var(--gray); border-color: var(--gray); }
    .btn-secondary:hover { color: #fff; background-color: var(--gray-hover); border-color: var(--gray-active); }
    .btn-secondary:active { color: #fff; background-color: var(--gray-active); border-color: #51585e; }

    .btn-danger { --ring: 225, 83, 97; color: #fff; background-color: var(--danger); border-color: var(--danger); }
    .btn-danger:hover { color: #fff; background-color: var(--danger-hover); border-color: #b02a37; }
    .btn-danger:active { color: #fff; background-color: var(--danger-active); border-color: #a52834; }

    .btn-outline-danger { --ring: 220, 53, 69; color: var(--danger); border-color: var(--danger); }
    .btn-outline-danger:hover { color: #fff; background-color: var(--danger); border-color: var(--danger); }

    .btn-close {
      box-sizing: content-box;
      width: 1em;
      height: 1em;
      padding: 0.25em;
      color: #000;
      background: transparent no-repeat center / 1em
        url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16' fill='%23000'%3e%3cpath d='M.293.293a1 1 0 0 1 1.414 0L8 6.586 14.293.293a1 1 0 1 1 1.414 1.414L9.414 8l6.293 6.293a1 1 0 0 1-1.414 1.414L8 9.414l-6.293 6.293a1 1 0 0 1-1.414-1.414L6.586 8 .293 1.707a1 1 0 0 1 0-1.414z'/%3e%3c/svg%3e");
      border: 0;
      border-radius: var(--radius);
      opacity: 0.5;
      cursor: pointer;
    }

    .btn-close:hover { opacity: 0.75; }
    .btn-close:focus-visible { opacity: 1; }

    .form-label {
      display: inline-block;
      margin-bottom: 0.5rem;
    }

    .form-control,
    .form-select {
      display: block;
      width: 100%;
      padding: 0.375rem 0.75rem;
      font-family: inherit;
      font-size: 1rem;
      font-weight: 400;
      line-height: 1.5;
      color: var(--body-color);
      background-color: var(--body-bg);
      border: 1px solid var(--border-color);
      border-radius: var(--radius);
      transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
    }

    .form-control::placeholder { color: rgba(33, 37, 41, 0.75); opacity: 1; }

    .form-control:focus,
    .form-select:focus {
      outline: 0;
      border-color: #86b7fe;
      box-shadow: 0 0 0 0.25rem rgba(13, 110, 253, 0.25);
    }

    .form-select {
      padding-right: 2.25rem;
      appearance: none;
      background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill='none' stroke='%23343a40' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='m2 5 6 6 6-6'/%3e%3c/svg%3e");
      background-repeat: no-repeat;
      background-position: right 0.75rem center;
      background-size: 16px 12px;
    }

    .invalid-feedback {
      display: none;
      width: 100%;
      margin-top: 0.25rem;
      font-size: 0.875em;
      color: var(--danger);
    }

    .form-control.is-invalid,
    .form-select.is-invalid,
    .was-validated .form-control:invalid,
    .was-validated .form-select:invalid {
      border-color: var(--danger);
    }

    .form-control.is-invalid:focus,
    .form-select.is-invalid:focus,
    .was-validated .form-control:invalid:focus,
    .was-validated .form-select:invalid:focus {
      border-color: var(--danger);
      box-shadow: 0 0 0 0.25rem rgba(220, 53, 69, 0.25);
    }

    .form-control.is-invalid ~ .invalid-feedback,
    .form-select.is-invalid ~ .invalid-feedback,
    .was-validated .form-control:invalid ~ .invalid-feedback,
    .was-validated .form-select:invalid ~ .invalid-feedback {
      display: block;
    }

    .form-control.is-valid,
    .form-select.is-valid,
    .was-validated .form-control:valid,
    .was-validated .form-select:valid {
      border-color: #198754;
    }

    .alert {
      position: relative;
      padding: 1rem;
      margin-bottom: 1rem;
      border: 1px solid transparent;
      border-radius: var(--radius);
    }

    .alert-success { color: #0a3622; background-color: #d1e7dd; border-color: #a3cfbb; }
    .alert-danger  { color: #58151c; background-color: #f8d7da; border-color: #f1aeb5; }
    .alert-warning { color: #664d03; background-color: #fff3cd; border-color: #ffe69c; }
    .alert-info    { color: #055160; background-color: #cff4fc; border-color: #9eeaf9; }

    .table-responsive {
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }

    .table {
      width: 100%;
      margin-bottom: 1rem;
      color: var(--body-color);
      vertical-align: top;
      border-color: var(--border-color);
      border-collapse: collapse;
    }

    .table th,
    .table td {
      padding: 0.5rem;
      text-align: left;
      border-bottom: 1px solid var(--border-color);
    }

    .table > thead { vertical-align: bottom; }
    .table > thead th { border-bottom: 2px solid currentcolor; }
    .table.align-middle > :not(caption) > * > * { vertical-align: middle; }

    .table-striped > tbody > tr:nth-of-type(odd) > * {
      background-color: rgba(0, 0, 0, 0.05);
    }

    .fade { transition: opacity 0.15s linear; }
    .fade:not(.show) { opacity: 0; }

    .modal {
      position: fixed;
      inset: 0;
      z-index: 1055;
      display: none;
      width: 100%;
      height: 100%;
      overflow-x: hidden;
      overflow-y: auto;
      outline: 0;
    }

    .modal-dialog {
      position: relative;
      width: auto;
      max-width: 500px;
      margin: 0.5rem;
      pointer-events: none;
    }

    @media (min-width: 576px) {
      .modal-dialog { margin: 1.75rem auto; }
    }

    .modal.fade .modal-dialog {
      transform: translate(0, -50px);
      transition: transform 0.3s ease-out;
    }

    .modal.show .modal-dialog { transform: none; }

    .modal-dialog-centered {
      display: flex;
      align-items: center;
      min-height: calc(100% - 1rem);
    }

    @media (min-width: 576px) {
      .modal-dialog-centered { min-height: calc(100% - 3.5rem); }
    }

    .modal-content {
      position: relative;
      display: flex;
      flex-direction: column;
      width: 100%;
      color: var(--body-color);
      background-color: var(--body-bg);
      border: 1px solid var(--border-translucent);
      border-radius: var(--radius-lg);
      outline: 0;
      pointer-events: auto;
    }

    .modal-header {
      display: flex;
      flex-shrink: 0;
      align-items: center;
      justify-content: space-between;
      padding: 1rem;
      border-bottom: 1px solid var(--border-color);
      border-top-left-radius: calc(var(--radius-lg) - 1px);
      border-top-right-radius: calc(var(--radius-lg) - 1px);
    }

    .modal-title { margin: 0; line-height: 1.5; }
    .modal-body { position: relative; flex: 1 1 auto; padding: 1rem; }

    .modal-footer {
      display: flex;
      flex-shrink: 0;
      flex-wrap: wrap;
      align-items: center;
      justify-content: flex-end;
      gap: 0.5rem;
      padding: 0.75rem;
      border-top: 1px solid var(--border-color);
    }

    .modal-backdrop {
      position: fixed;
      inset: 0;
      z-index: 1050;
      width: 100vw;
      height: 100vh;
      background-color: #000;
    }

    .modal-backdrop.fade { opacity: 0; }
    .modal-backdrop.show { opacity: 0.5; }

    body.modal-open { overflow: hidden; }

    .me-1       { margin-right: 0.25rem !important; }
    .text-end   { text-align: right !important; }
    .text-nowrap { white-space: nowrap !important; }

    .alert-dismissible { padding-right: 3rem; }

    .alert-dismissible .btn-close {
      position: absolute;
      top: 0;
      right: 0;
      z-index: 2;
      padding: 1.25rem 1rem;
    }

    .btn-outline-primary { color: var(--blue); border-color: var(--blue); }
    .btn-outline-primary:hover { color: #fff; background-color: var(--blue); border-color: var(--blue); }
    .btn-outline-primary:active { color: #fff; background-color: var(--blue-active); border-color: var(--blue-active); }

    .table > tbody > tr.table-primary > * {
      color: #000;
      background-color: #cfe2ff;
      border-color: #bacbe6;
    }

    @media (prefers-reduced-motion: reduce) {
      *,
      *::before,
      *::after {
        transition-duration: 0.01ms !important;
        animation-duration: 0.01ms !important;
      }
    }
  </style>
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
