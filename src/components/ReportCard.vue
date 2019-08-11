<template>
  <div class="container">
    
    <section class="container head">
      <div class="columns header is-mobile"> 
        <div class="column is-half-mobile is-one-fifth-desktop"> 
          <img class="image" src="../assets/telios.png">
        </div>
        <div class="column is-half-mobile is-four-fifths-desktop has-text-centered h1-text"> 
          <h1 class="is-size-1 is-size-4-mobile"><strong>Report Card</strong></h1>
        </div>
      </div>
    </section>

    <section class="container student-info">
      <div>
        <div class="field is-horizontal">
          <div class="field-label is-normal">
            <label class="label">Name</label>
          </div>
          <div class="field-body">
            <div class="field">
              <div class="control">
                <input v-model="student_name" class="input" type="text" placeholder="Student's Name">
              </div>
            </div>
          </div>
        </div>

        <div class="field is-horizontal">
          <div class="field-label is-normal">
            <label class="label">Student Grade</label>
          </div>
          <div class="field-body">
            <div class="field">
              <div class="control">
                <input v-model="current_grade" class="input" type="text" placeholder="Enter Current Grade">
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>


    <section class="container grade-info">
      <div class="box"> 
        <table id="course_results" class="table" width="100%">
          <thead>
            <tr>
              <th><abbr title="Index">Index</abbr></th>
              <th width="70%">Course Title</th>
              <th><abbr title="Score">Score</abbr></th>
              <th><abbr title="Grade">Grade</abbr></th>
            </tr>
          </thead>
          <tfoot>
            <tr>
              <th><abbr title="Index">Index</abbr></th>
              <th>Course Title</th>
              <th><abbr title="Score">Score</abbr></th>
              <th><abbr title="Grade">Grade</abbr></th>
            </tr>
          </tfoot>
          <tbody>
            <tr>
              <th>1</th>
              <td><a href="#">Mathematics</a>
              </td>
              <td><input v-model="courses.math.score" class="input" type="text"></td>
              <td>
                <select>
                  <option >Select Grade</option>
                  <option :selected="courses.math.score >= 70 ? true:false" value="A">A</option>
                  <option :selected="courses.math.score < 70 && courses.math.score >= 60 ? true:false" value="B">B</option>
                  <option :selected="courses.math.score < 60 && courses.math.score >= 55 ? true:false" value="C">C</option>
                  <option :selected="courses.math.score < 55 && courses.math.score >= 50 ? true:false" value="D">D</option>
                  <option :selected="courses.math.score < 50 && courses.math.score >= 45 ? true:false" value="E">E</option>
                  <option :selected="courses.math.score < 45 ? true:false" value="F">F</option>
                </select>
              </td>
            </tr>
            <tr>
              <th>2</th>
              <td><a href="#">English</a>
              </td>
              <td><input class="input" v-model="courses.eng.score" type="text"></td>
              <td>
                <select>
                  <option >Select Grade</option>
                  <option :selected="courses.eng.score >= 70 ? true:false" value="A">A</option>
                  <option :selected="courses.eng.score < 70 && courses.eng.score >= 60 ? true:false" value="B">B</option>
                  <option :selected="courses.eng.score < 60 && courses.eng.score >= 55 ? true:false" value="C">C</option>
                  <option :selected="courses.eng.score < 55 && courses.eng.score >= 50 ? true:false" value="D">D</option>
                  <option :selected="courses.eng.score < 50 && courses.eng.score >= 45 ? true:false" value="E">E</option>
                  <option :selected="courses.eng.score < 45 ? true:false" value="F">F</option>
                </select>
              </td>
            </tr>
            <tr>
              <th>3</th>
              <td><a href="#">Biology</a>
              </td>
              <td><input class="input" v-model="courses.bio.score" type="text"></td>
              <td>
                <select>
                  <option >Select Grade</option>
                  <option :selected="courses.bio.score >= 70 ? true:false" value="A">A</option>
                  <option :selected="courses.bio.score < 70 && courses.bio.score >= 60 ? true:false" value="B">B</option>
                  <option :selected="courses.bio.score < 60 && courses.bio.score >= 55 ? true:false" value="C">C</option>
                  <option :selected="courses.bio.score < 55 && courses.bio.score >= 50 ? true:false" value="D">D</option>
                  <option :selected="courses.bio.score < 50 && courses.bio.score >= 45 ? true:false" value="E">E</option>
                  <option :selected="courses.bio.score < 45 ? true:false" value="F">F</option>
                </select>
              </td>
            </tr>
            <tr>
              <th>4</th>
              <td><a href="#">Chemistry</a>
              </td>
              <td><input class="input" v-model="courses.chem.score" type="text"></td>
              <td>
                <select>
                  <option >Select Grade</option>
                  <option :selected="courses.chem.score >= 70 ? true:false" value="A">A</option>
                  <option :selected="courses.chem.score < 70 && courses.chem.score >= 60 ? true:false" value="B">B</option>
                  <option :selected="courses.chem.score < 60 && courses.chem.score >= 55 ? true:false" value="C">C</option>
                  <option :selected="courses.chem.score < 55 && courses.chem.score >= 50 ? true:false" value="D">D</option>
                  <option :selected="courses.chem.score < 50 && courses.chem.score >= 45 ? true:false" value="E">E</option>
                  <option :selected="courses.chem.score < 45 ? true:false" value="F">F</option>
                </select>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <div class="columns">
      <div class="column is-full is-centered"><a @click=generatepdf() class="button is-primary is-outlined">Generate PDF</a></div>
    </div>
  </div>
</template>

<script>
import jsPDF from 'jspdf';
import 'jspdf-autotable';
(function(API) {
    API.textAlign = function(txt, options, x, y) {
        options = options || {};
        // Use the options align property to specify desired text alignment
        // Param x will be ignored if desired text alignment is 'center'.
        // Usage of options can easily extend the function to apply different text
        // styles and sizes

        // Get current font size
        var fontSize = this.internal.getFontSize();

        // Get page width
        var pageWidth = this.internal.pageSize.width;

        // Get the actual text's width
        // You multiply the unit width of your string by your font size and divide
        // by the internal scale factor. The division is necessary
        // for the case where you use units other than 'pt' in the constructor
        // of jsPDF.

        var txtWidth = this.getStringUnitWidth(txt) * fontSize / this.internal.scaleFactor;

        if (options.align === "center") {

            // Calculate text's x coordinate
            x = (pageWidth - txtWidth) / 2;

        } else if (options.align === "centerAtX") { // center on X value

            x = x - (txtWidth / 2);

        } else if (options.align === "right") {

            x = x - txtWidth;
        }

        // Draw text at x,y
        this.text(txt, x, y);
    };
    /*
        API.textWidth = function(txt) {
          var fontSize = this.internal.getFontSize();
            return this.getStringUnitWidth(txt)*fontSize / this.internal.scaleFactor;
        };
    */

    API.getLineHeight = function(txt) {
        return this.internal.getLineHeight();
    };

})(jsPDF.API);
export default {
  name: 'ReportCard',
  props: {
    msg: String
  },
  data() {

    return {
        student_name: '',
        current_grade: '',
        page_size: 'a4',
        telios_logo: { 
            src: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA8AAAAEsCAYAAAAMz9pLAAAACXBIWXMAAAsTAAALEwEAmpwYAAAGtmlUWHRYTUw6Y29tLmFkb2JlLnhtcAAAAAAAPD94cGFja2V0IGJlZ2luPSLvu78iIGlkPSJXNU0wTXBDZWhpSHpyZVN6TlRjemtjOWQiPz4gPHg6eG1wbWV0YSB4bWxuczp4PSJhZG9iZTpuczptZXRhLyIgeDp4bXB0az0iQWRvYmUgWE1QIENvcmUgNS42LWMxNDIgNzkuMTYwOTI0LCAyMDE3LzA3LzEzLTAxOjA2OjM5ICAgICAgICAiPiA8cmRmOlJERiB4bWxuczpyZGY9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkvMDIvMjItcmRmLXN5bnRheC1ucyMiPiA8cmRmOkRlc2NyaXB0aW9uIHJkZjphYm91dD0iIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtbG5zOmRjPSJodHRwOi8vcHVybC5vcmcvZGMvZWxlbWVudHMvMS4xLyIgeG1sbnM6cGhvdG9zaG9wPSJodHRwOi8vbnMuYWRvYmUuY29tL3Bob3Rvc2hvcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RFdnQ9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZUV2ZW50IyIgeG1wOkNyZWF0b3JUb29sPSJBZG9iZSBQaG90b3Nob3AgQ0MgKFdpbmRvd3MpIiB4bXA6Q3JlYXRlRGF0ZT0iMjAxOC0wNy0xN1QxMTo1Njo0OCswMTowMCIgeG1wOk1vZGlmeURhdGU9IjIwMTgtMDctMjdUMTM6MzE6NDYrMDE6MDAiIHhtcDpNZXRhZGF0YURhdGU9IjIwMTgtMDctMjdUMTM6MzE6NDYrMDE6MDAiIGRjOmZvcm1hdD0iaW1hZ2UvcG5nIiBwaG90b3Nob3A6Q29sb3JNb2RlPSIzIiBwaG90b3Nob3A6SUNDUHJvZmlsZT0ic1JHQiBJRUM2MTk2Ni0yLjEiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6Y2IxYmY2MzItYzMyNC1mMTQ4LWJjYjItOWNhYjdlYmRhNjA2IiB4bXBNTTpEb2N1bWVudElEPSJhZG9iZTpkb2NpZDpwaG90b3Nob3A6ZmQ1OWQwMjgtYzE3My1lOTQ4LWIyNzYtOWZkNWI2OTc1ZjkwIiB4bXBNTTpPcmlnaW5hbERvY3VtZW50SUQ9InhtcC5kaWQ6ZTE4YTdjZTItNGNhMS1lMTRhLTg2ZjMtYjRmZTUxY2JkNzZhIj4gPHhtcE1NOkhpc3Rvcnk+IDxyZGY6U2VxPiA8cmRmOmxpIHN0RXZ0OmFjdGlvbj0iY3JlYXRlZCIgc3RFdnQ6aW5zdGFuY2VJRD0ieG1wLmlpZDplMThhN2NlMi00Y2ExLWUxNGEtODZmMy1iNGZlNTFjYmQ3NmEiIHN0RXZ0OndoZW49IjIwMTgtMDctMTdUMTE6NTY6NDgrMDE6MDAiIHN0RXZ0OnNvZnR3YXJlQWdlbnQ9IkFkb2JlIFBob3Rvc2hvcCBDQyAoV2luZG93cykiLz4gPHJkZjpsaSBzdEV2dDphY3Rpb249InNhdmVkIiBzdEV2dDppbnN0YW5jZUlEPSJ4bXAuaWlkOjEzMjFjZjMyLTMxM2YtMDQ0OS05YjhkLWNhYjhmNjkzMzg1ZiIgc3RFdnQ6d2hlbj0iMjAxOC0wNy0yN1QxMzoyMTozMiswMTowMCIgc3RFdnQ6c29mdHdhcmVBZ2VudD0iQWRvYmUgUGhvdG9zaG9wIENDIChXaW5kb3dzKSIgc3RFdnQ6Y2hhbmdlZD0iLyIvPiA8cmRmOmxpIHN0RXZ0OmFjdGlvbj0ic2F2ZWQiIHN0RXZ0Omluc3RhbmNlSUQ9InhtcC5paWQ6Y2IxYmY2MzItYzMyNC1mMTQ4LWJjYjItOWNhYjdlYmRhNjA2IiBzdEV2dDp3aGVuPSIyMDE4LTA3LTI3VDEzOjMxOjQ2KzAxOjAwIiBzdEV2dDpzb2Z0d2FyZUFnZW50PSJBZG9iZSBQaG90b3Nob3AgQ0MgKFdpbmRvd3MpIiBzdEV2dDpjaGFuZ2VkPSIvIi8+IDwvcmRmOlNlcT4gPC94bXBNTTpIaXN0b3J5PiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/PjuJ9WgAADfWSURBVHja7d39pxzp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',
            w: '960',
            h: '300'
            },
        page_width: 210, // mm
        page_margin: 10,
        content_width: 190,
        courses: {
          math: {score: '', grade: '',},
          eng: {score: '', grade: '',},
          bio: {score: '', grade: '',},
          chem: {score: '', grade: '',},
        },
      }
  },
  methods: {

    imgSizes(img_w, img_h, img_mm_w) {
      /*
      img_w and img_h represent the original image size, in pixel
      img_mm_w is the desidered rendered image size, in millimeters

      */

            if (img_mm_w > this.content_width) { // this should be never used...
                img_mm_w = this.content_width;
            }

            if (this.mm2px(img_mm_w) > img_w) {
                throw 'The `img_mm_w` parameter is too big';
            }

            var img_mm_h = Math.round((this.px2mm(img_h) * img_mm_w) / this.px2mm(img_w));

            return {
                w: img_mm_w,
                h: img_mm_h,
                centered_x: (this.page_width - img_mm_w) / 2
            };
    },
    px2mm(pixel) {
            // px to inches
            var inches = pixel / 72;
            return inches * 25.4;
    },

    mm2px(millimeters) {
        // mm to inches
        var inches = millimeters / 25.4;
        return inches * 72;
    },
    generatepdf() {
      var pdf = new jsPDF('p', 'mm', this.page_size),
                text_baseline,

                // some colors:
                light_grey = 237,
                grey = 128,
                black = 0,
                white = 255,
                vspace = 10;

            // Optional - set properties of the document
            pdf.setProperties({
                title: this.student_name + ' Score Report',
                subject: 'Grades',
                author: 'Telios',
                creator: 'Telios PDF'
            });

            // fonts initializing
            pdf.setFont("helvetica");
            pdf.setFontType("bold");

            //telios logo
            var box_height = 25;
            var _y = 0;
            var lineHeight = 0;
            var lineWidth = 0;
            var data = [];
            var headers = [];
            var config = {};
            var _x = 10;
            var _string = '';

                pdf.setFillColor(183, 69, 121);
                pdf.rect(this.page_margin, _y, this.content_width, box_height, 'F');
                pdf.setFontSize(60);
                pdf.setTextColor(white);

                // y_correction: value to be added to y coord of the grey box to have text vertically centered
                // it is empirically calculated adding 1/3 of text line height to half box height
                var logo_sizes = this.imgSizes(this.telios_logo.w, this.telios_logo.h, 80);
                pdf.addImage(this.telios_logo.src, 'PNG', logo_sizes.centered_x, _y, logo_sizes.w, logo_sizes.h);

                _y += box_height + vspace;

            // report card
            pdf.setTextColor(183, 69, 121);
            pdf.setFontSize(22);
            pdf.setFontType("italic");
            _string = 'Student Report Card'
            lineHeight = this.px2mm(pdf.getLineHeight(_string));

            pdf.textAlign(_string, {
                align: "center"
            }, 10, _y);

            _y += (20+lineHeight);

            pdf.setTextColor(black)
            _string = 'Student Name:'
            pdf.setFontSize(25);
            pdf.setFontType("bold");
            lineHeight = this.px2mm(pdf.getLineHeight(_string));
            pdf.textAlign(_string, {
                align: "left"
            }, 10, _y);

            lineWidth = this.px2mm(pdf.getTextWidth(_string));
            _string = this.student_name;
            pdf.setFontSize(20);
            pdf.setFontType("normal");
            pdf.textAlign(_string, {
                align: "left"
            }, lineWidth + 15, _y);

            _y += vspace + lineHeight;

            _string = 'Current Grade:'
            pdf.setFontSize(25);
            pdf.setFontType("bold");
            lineHeight = this.px2mm(pdf.getLineHeight(_string));
            pdf.textAlign(_string, {
                align: "left"
            }, 10, _y);

            lineWidth = this.px2mm(pdf.getTextWidth(_string));
            _string = this.current_grade;
            pdf.setFontSize(20);
            pdf.setFontType("normal");
            pdf.textAlign(_string, {
                align: "left"
            }, _x + lineWidth + 15, _y);

            _y += vspace + lineHeight;
          var header= [
          [ 'Index', 'Course', 'Score', 'Grade' ]
          ];
          var body = [
            ['1','Mathematics',this.courses.math.score,this.courses.math.grade ],
            ['2','English',this.courses.eng.score,this.courses.eng.grade ],
            ['3','Biology',this.courses.bio.score,this.courses.bio.grade ],
            ['4','CHemistry',this.courses.chem.score,this.courses.chem.grade ],
          ];
            
                pdf.autoTable({startX:10, startY:_y, head: header, body: body});
                pdf.save(this.student_name +"'s" + ' Score Report' + '.pdf');
      }

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.image {
  width: 100%;
}
.student-info {
  margin-top:20px;
  margin-bottom:20px;
  padding:5px;
}
.grade-info {
  padding:5px;
  margin-bottom: 20px;
}
.head {
  margin-bottom: 90px;
}
.header {
  background-color: rgb(183, 69, 121);
}
.h1-text {
}
h1 {
  font-size: 30px;
  text-align: right;
  color: white;
}
strong {
  color:white;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
