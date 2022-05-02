# MATLAB-physics-project
This code is for a matlab gui that I'm trying to create, that given the cars weight, radius of a road curve, and the banking angle of the curve, code should produce the cars max speed it's able to go along the curve.
This code is for a gui with the three edit fields shown for the radius, banking angle, and car weight.
classdef app1 < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        UIFigure                    matlab.ui.Figure
        PlotButton                  matlab.ui.control.Button
        CurvebankingangleEditField  matlab.ui.control.NumericEditField
        CurvebankingangleEditFieldLabel  matlab.ui.control.Label
        CurveradiusEditField        matlab.ui.control.NumericEditField
        CurveradiusEditFieldLabel   matlab.ui.control.Label
        CarweightEditField          matlab.ui.control.NumericEditField
        CarweightEditFieldLabel     matlab.ui.control.Label
        UIAxes                      matlab.ui.control.UIAxes
    end

    
    properties (Access = public)
        g=9.8
        mu=1
        r=0:10:5000
        speed=sqrt(r*g(sin(app.CurvebankingangleEditField.Value)*mu.cos...
         (app.CurvebankingangleEditField.Value))/(cos...
         (app.CurvebankingangleEditField.Value)-mu*sin...
         (app.CurvebankingangleEditField.Value)));
    
    methods (Access = private)
        
        function results = func(app)
            
        end
    end
    end

    % Callbacks that handle component events
    methods (Access = private)

        % Button down function: UIAxes
        function UIAxesButtonDown(app, event)
            x= 0:1:30
            y= app.speed
            plot(app.UIAxes,x,y)
        end
    end

    % Component initialization
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create UIFigure and hide until all components are created
            app.UIFigure = uifigure('Visible', 'off');
            app.UIFigure.Position = [100 100 640 480];
            app.UIFigure.Name = 'MATLAB App';

            % Create UIAxes
            app.UIAxes = uiaxes(app.UIFigure);
            title(app.UIAxes, 'Title')
            xlabel(app.UIAxes, 'Time')
            ylabel(app.UIAxes, 'Speed')
            zlabel(app.UIAxes, 'Z')
            app.UIAxes.XTickLabel = {'0'; '10'; '20'; '30'; '40'; '50'};
            app.UIAxes.YTickLabel = {'0'; '50'; '100'};
            app.UIAxes.ButtonDownFcn = createCallbackFcn(app, @UIAxesButtonDown, true);
            app.UIAxes.Position = [302 198 300 185];

            % Create CarweightEditFieldLabel
            app.CarweightEditFieldLabel = uilabel(app.UIFigure);
            app.CarweightEditFieldLabel.HorizontalAlignment = 'right';
            app.CarweightEditFieldLabel.Position = [34 332 63 22];
            app.CarweightEditFieldLabel.Text = 'Car weight';

            % Create CarweightEditField
            app.CarweightEditField = uieditfield(app.UIFigure, 'numeric');
            app.CarweightEditField.Position = [112 332 100 22];

            % Create CurveradiusEditFieldLabel
            app.CurveradiusEditFieldLabel = uilabel(app.UIFigure);
            app.CurveradiusEditFieldLabel.HorizontalAlignment = 'right';
            app.CurveradiusEditFieldLabel.Position = [26 279 74 22];
            app.CurveradiusEditFieldLabel.Text = 'Curve radius';

            % Create CurveradiusEditField
            app.CurveradiusEditField = uieditfield(app.UIFigure, 'numeric');
            app.CurveradiusEditField.Position = [115 279 100 22];

            % Create CurvebankingangleEditFieldLabel
            app.CurvebankingangleEditFieldLabel = uilabel(app.UIFigure);
            app.CurvebankingangleEditFieldLabel.HorizontalAlignment = 'right';
            app.CurvebankingangleEditFieldLabel.Position = [7 208 116 22];
            app.CurvebankingangleEditFieldLabel.Text = 'Curve banking angle';

            % Create CurvebankingangleEditField
            app.CurvebankingangleEditField = uieditfield(app.UIFigure, 'numeric');
            app.CurvebankingangleEditField.Position = [138 208 100 22];

            % Create PlotButton
            app.PlotButton = uibutton(app.UIFigure, 'push');
            app.PlotButton.Position = [214 163 100 22];
            app.PlotButton.Text = 'Plot';

            % Show the figure after all components are created
            app.UIFigure.Visible = 'on';
        end
    end

    % App creation and deletion
    methods (Access = public)

        % Construct app
        function app = app1

            % Create UIFigure and components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.UIFigure)

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.UIFigure)
        end
    end
end
