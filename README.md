# Android-Using-Calcultor
I have done a calculator app using Android Studio
package com.example.calculator;

import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;

class MainActivity extends AppCompatActivity {

    TextView workingTV, resultsTV;
    String workings = "";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);

        initTextViews();
    }

    private void initTextViews() {
        workingTV = findViewById(R.id.workingTextView);
        resultsTV = findViewById(R.id.resultsTextView);
    }

    private void setWorkings(String givenValue) {
        workings = workings + givenValue;
        workingTV.setText(workings);
    }

    public void divisionOnClick(View view) {
        setWorkings("/");
    }

    public void mulOnClick(View view) {
        setWorkings("*");
    }

    public void addOnClick(View view) {
        setWorkings("+");
    }

    public void subOnClick(View view) {
        setWorkings("-");
    }

    public void percentageOnClick(View view) {
        setWorkings("%");
    }

    public void oneOnClick(View view) {
        setWorkings("1");
    }

    public void twoOnClick(View view) {
        setWorkings("2");
    }

    public void threeOnClick(View view) {
        setWorkings("3");
    }

    public void fourOnClick(View view) {
        setWorkings("4");
    }

    public void fiveOnClick(View view) {
        setWorkings("5");
    }
    // power off operator - '^'
    //2^3=8=2*2*2
    //'^' XoR operator

    //Math.pow(2,3)=8

    String formula = "";
    String tempFormula = "";
   private void CheckForPower() {
        ArrayList<Integer> indexOfPowers = new ArrayList<>();//5
       for(int i=0;i<workings.length();i++) {
           if(workings.charAt(i) == '^') {
              indexOfPowers.add(i);
           }
       }
       formula = workings;
       tempFormula = workings;
       for (Integer index: indexOfPowers) {
           changeFormula(index);
       }
       formula = tempFormula;
   }
   private void changeFormula(Integer index) {
        String numberLeft = "";
        String numberRight = "";

        for(int i = index+1; i<workings.length(); i++) {
            if (isNumeric(workings.charAt(i))) {
                numberRight = numberRight + workings.charAt(i);
            }
            else {
                break;
            }
        }
        for (int i = index-1;i>=0;i--) {
            if (isNumeric(workings.charAt(i))) {
                numberLeft = workings.charAt(i) + numberLeft;
            }
            else {
                break;
            }
        }
        String original = numberLeft +"^" +numberRight; //55^23
        String changed = "Math.pow("+numberLeft+","+numberRight+")"; //Math.pow(55,23);
       tempFormula = tempFormula.replace(original, changed);
    }
    private boolean isNumeric(char ch) {
       return (ch <= '9' && ch >= '0') || ch == '_';
    }
}



