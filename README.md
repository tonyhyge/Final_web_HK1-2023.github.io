<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://kit.fontawesome.com/e8ec9aa329.js" crossorigin="anonymous"></script>
    <link rel="stylesheet" href="style.css">
    <title>Document</title>
</head>
<body>
    <div class="container">
        <div class="profile-area">
            <div class="task-manager">Task manager</div>
            <div class="side-wrapper">
                <div class="user-profile">
                    <img src="user1.png" alt="user-image" class="user-image">
                    <div class="user-name">
                        <b>Quang Minh Pham</b>
                    </div>
                    <div class="user-email">minhphamtony@gmail.com</div>
                </div>
                <div class="user-notifications">
                    <div class="notify">
                        <i class="fa-sharp fa-solid fa-gear"></i>
                    </div>
                    <div class="notify alert">
                        <i class="fa-solid fa-envelope"></i>
                    </div>
                    <div class="notify alert">
                        <i class="fa-sharp fa-solid fa-bell"></i>
                    </div>
                </div>
                <div class="progress-status">10/53</div>
                <div class="progress">
                    <div class="progress-bar"></div>
                </div>
                <div class="task-status">
                    <div class="task-stat">
                        <div class="task-number">10</div>
                        <div class="task-condition">Completed</div>
                        <div class="task-tasks"></div>
                    </div>
                    <div class="task-stat">
                        <div class="task-number">22</div>
                        <div class="task-condition">to do</div>
                        <div class="task-tasks"></div>
                    </div>
                    <div class="task-stat">
                        <div class="task-number">53</div>
                        <div class="task-condition">All</div>
                        <div class="task-tasks"></div>
                    </div>
                </div>
            </div>
            <div class="side-wrapper">
                <div class="tag-title">Tags</div>
                <div class="tag-name">
                    <div class="tag">School</div>
                    <div class="tag">Work</div>
                    <div class="tag">Event</div>
                    <div class="tag">Personal</div>
                </div>
            </div>
        </div>
        <div class="main-area">
            <div class="header">
                <div class="search-bar">
                    <input type="text" placeholder="Search...">
                </div>
                <div class="calendar-todolist">
                    <input type="checkbox" class="calendar-todolist-checkbox">
                    <div class="toggle-page">
                        <span>Calendar</span>
                    </div>
                    <div class="layer"></div>
                </div>
                <div class="color-menu">
                    <i class="fa-solid fa-paint-roller"></i>
                    <input type="color" value="#4d76fd" class="colorpicker">
                </div>
            </div>
            <div class="main-container">
                <div class="left-main-container">
                    <div class="clendar-container">
                        <div class="calendar">
                            <div class="month">
                                <i class="fas fa-angle-left prev"></i>
                                <div class="date"></div>
                                <i class="fas fa-angle-right next"></i>
                            </div>
                            <div class="weekdays">
                                <div>Sun</div>
                                <div>Mon</div>
                                <div>Tue</div>
                                <div>Wed</div>
                                <div>Thu</div>
                                <div>Fri</div>
                                <div>Sat</div>
                            </div>
                            <div class="days"></div>
                            <div class="goto-today">
                                <div class="goto">
                                    <input type="text" placeholder="mm/yyyy" class="date-input" />
                                    <button class="goto-btn">Go</button>
                                </div>
                                <button class="today-btn">Today</button>
                            </div>
                        </div>
                    </div>
                    <div class="add-event-wrapper  ">
                        <div class="add-event-header">
                            <div class="title">Add Event</div>
                            <i class="fas fa-times close"></i>
                        </div>
                        <div class="add-event-body">
                            <div class="add-event-input">
                                <input type="text" placeholder="Event Name" class="event-name">
                            </div>
                            <div class="add-event-input">
                                <input id="pac-input"type="text" placeholder="Location" class="event-location">
                                <button class="add-event-btn-map " ><i class="fa-sharp fa-solid fa-location-dot"></i></button>
                                <div id="googleMap" class="map  ">
                                    <script
                                    src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC69dkDskDMsxSvZiCqAd9thxLDBohuBJI&callback=initAutocomplete&libraries=places&v=weekly"
                                    defer
                                  ></script>
                                </div>
                            </div>
                            <div class="add-event-input">
                                <input type="text" placeholder="From" class="event-from">
                                <input type="text" placeholder="To" class="event-to">
                            </div>
                            <div class="add-event-input">
                                <input type="text" placeholder="Note" class="event-note">
                            </div>
                            <div class="add-event-footer">
                                <button class="add-event-btn">ADD EVENT</button>
                            </div>
                        </div>
                    </div>
                    <div class="todolist">
                        <div class="todolist-tab anim-y">
                        <?php
                            include_once ("db_config.php");
                            $con = mysqli_connect(DB_HOST, DB_USER, DB_PASS, DB_NAME, DB_CONNECTION);
                            $q = intval($_GET['q']);
                            if (!$con) {
                            die('Could not connect: ' . mysqli_connect_error());
                            }
                            mysqli_select_db($con,"ajax_demo");
                            $sql="SELECT * FROM events";
                            $result = mysqli_query($con,$sql);
                            echo "<table class='todolist-table' >
                            <tr>
                            <th>day</th>
                            <th>month</th>
                            <th>year</th>
                            <th>title</th>
                            <th>location</th>
                            <th>time</th>
                            </tr>";
                            while($row = mysqli_fetch_array($result)) {
                            echo "<tr>";
                            echo "<td>" . $row['day'] . "</td>";
                            echo "<td>" . $row['month'] . "</td>";
                            echo "<td>" . $row['year'] . "</td>";
                            echo "<td>" . $row['title'] . "</td>";
                            echo "<td>" . $row['location'] . "</td>";
                            echo "<td>" . $row['time'] . "</td>";
                            echo "</tr>";
                            }
                            echo "</table>";
                            mysqli_close($con);
                            ?>
                        </div>                            
                    </div>
                </div>
                <div class="right-main-container">
                    <div class="today-date">
                        <div class="event-day">Friday</div>
                        <div class="event-date">10 November 2023</div>
                    </div>
                    <div class="events">
                    </div>
                    <button class="add-event">
                        NEW TASK
                    </button>
                </div>
            </div>
        </div>
    </div>
    </div>
    </div>
    </div>
    <script src="script.js"></script>
</body>
</html>
