# Burger-Order

Public Class frmBurger

    Dim toppings As String = "You ordered a "
    Dim toppingOrdered As Boolean = False
    Dim burgerType As String
    Dim customerName, address As String

    Const BURGER_COST As Decimal = 2.99
    Const CHEESEBURGER_COST As Decimal = 3.79
    Const TURKEY_BURGER_COST As Decimal = 3.99
    Const FRIES_COST As Decimal = 1.99
    Const SODA_COST As Decimal = 1.49
    Const TAX_RATE As Decimal = 0.07
    Const LARGE_SODA As Decimal = 1.99
    Const SMALL_SODA As Decimal = 1.79
    Dim subtotal, salesTax, total As Decimal
    Dim orderOutput As String



    Private Sub btnOrder_Click(sender As Object, e As EventArgs) Handles btnOrder.Click
        burgerType = cbxBurgerType.Text

        Dim fries, soda, bacon As DialogResult
        bacon = MsgBox("Would you like to add crisp bacon to your order?", MsgBoxStyle.YesNo)
        fries = MsgBox("Do you want to add fries?", MsgBoxStyle.YesNo)
        soda = MsgBox("Do you want to add a soda?", MsgBoxStyle.YesNo)



        customerName = customerName.ToUpper()
        listOrder.Items.Add(customerName)
        listOrder.Items.Add(address)
        listOrder.Items.Add("")

        listOrder.Items.Add(burgerType)


        If bacon = Windows.Forms.DialogResult.Yes Then
            subtotal += 0.5
            listOrder.Items.Add("-bacon")
        End If
        If cbxKetchup.Checked Then
            listOrder.Items.Add("-ketchup")
        End If
        If cbxMustard.Checked Then
            listOrder.Items.Add("-mustard")
        End If
        If cbxBuffaloSauce.Checked Then
            listOrder.Items.Add("-buffalo sauce")
        End If

        If cbxLettuce.Checked Then
            listOrder.Items.Add("-lettuce")
            toppingOrdered = True
        End If
        If cbxOnions.Checked Then
            listOrder.Items.Add("-onions")
            toppingOrdered = True
        End If
        If cbxPickles.Checked Then
            listOrder.Items.Add("-pickles")
            toppingOrdered = True
        End If
        If cbxTomato.Checked Then
            listOrder.Items.Add("-tomatoes")
            toppingOrdered = True
        End If
        If toppingOrdered = False Then
            listOrder.Items.Add("-no toppings")
        End If

        listOrder.Items.Add("")


        If fries = Windows.Forms.DialogResult.Yes Then
            subtotal += FRIES_COST
            listOrder.Items.Add("  - Fries")
        End If

        If soda = Windows.Forms.DialogResult.Yes Then
            groupSoda.Visible = True
            groupToppings.Visible = False
        Else
            listOrder.Visible = True
            groupToppings.Visible = False
        End If

        btnFinish.Visible = True

    End Sub

    Private Sub frmBurgers_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        MsgBox("Welcome to Burgers R Us" & Chr(13) & "ENJOY", MsgBoxStyle.Information, "Burgers R Us")
        customerName = InputBox("What is your name?", "Intro")
        address = InputBox("What is your address")
    End Sub

    Private Sub cbxBurgerType_SelectedIndexChanged(sender As Object, e As EventArgs) Handles cbxBurgerType.SelectedIndexChanged
        groupToppings.Visible = True
    End Sub

    Private Sub btnFinish_Click(sender As Object, e As EventArgs) Handles btnFinish.Click
        btnFinish.Visible = False
        listOrder.Visible = True

        If burgerType = "Hamburger" Then
            subtotal += BURGER_COST
        ElseIf burgerType = "Cheeseburger" Then
            subtotal += CHEESEBURGER_COST
        Else
            subtotal = TURKEY_BURGER_COST
        End If

        If rbtLarge.Checked = True Then
            listOrder.Items.Add("  - Large Soda")
            subtotal += LARGE_SODA
        ElseIf rbtSmall.Checked = True Then
            subtotal += SMALL_SODA
            listOrder.Items.Add("  - Small Soda")
        End If

        salesTax = subtotal * TAX_RATE
        total = subtotal + salesTax



        orderOutput = "SubTotal: $" & Math.Round(subtotal, 2) & Chr(13) & _
        "Tax: $" & Math.Round(salesTax, 2) & Chr(13) & "Total: $" & Math.Round(total, 2)

        Dim correct As DialogResult
        correct = MsgBox("Is your order correct?", MsgBoxStyle.Question Or MsgBoxStyle.YesNo, "Correct?")
        If correct = Windows.Forms.DialogResult.Yes Then
            MsgBox("Thank you.  Your order comes to:" & Chr(13) & orderOutput, MsgBoxStyle.OkOnly)
            Me.Close()
        Else
            MsgBox("Sorry, lets try again", MsgBoxStyle.OkOnly)
            Application.Restart()
        End If
    End Sub
End Class
